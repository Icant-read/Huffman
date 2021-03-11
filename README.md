# Huffman

package binaryTrees;

import java.io.File;

import java.io.FileWriter;

import java.io.PrintStream;

import java.util.ArrayList;

import java.util.Comparator;

import java.util.HashMap;

import java.util.List;

import java.util.PriorityQueue;

import java.util.Queue;

import java.util.Scanner;

import java.util.TreeMap;

public class HuffmanTree {
	private Node root;
	
	public HuffmanTree(int[] frequencies) {
		compressString(frequencies);
	}
	//
	public static String compressString(int[] frequencies) {
		List<Node> nodes = makeNodes(frequencies);
		//make tree inputs '95' instead of '*' but that actually works fine, problem is that it is in the wrong order
		Node huffmanTree = makeTree(nodes);
		Node p = huffmanTree; System.out.println(printInOrder(p,"")); //prints a copy of huffman tree in order
		HashMap<Character, String> hashMap = makeHash(huffmanTree);
		String compressedString = makeCompress(frequencies, hashMap);
		System.out.println(translate(huffmanTree, "000100", 4));
		return compressedString;
	}

	public static String printInOrder(Node n, String s) {
		if(n!=null) {
			   s =printInOrder(n.l, s);
			   s+=(n.data + " ");
			   s =printInOrder(n.r, s);
		   }
		return s;
	}

	public static List<Node> makeNodes(int[] s) {
		List<Node> nodes = new ArrayList<>();

		for(int i = 0; i < s.length; i = i + 1) {
			Node temp = new Node(s[i], 1);
			int index = -1;
			for(int u = 0; u < nodes.size(); u++) {
				if(nodes.get(u) == temp) {
					index = u;
					break;
				}
			}
			if(index != -1) {
				nodes.get(index).data += 1;
			} else {
				nodes.add(temp);
			}
		}
		return nodes;
	}

	public static Node makeTree(List<Node> nodes) {
		PriorityQueue<Node> priorityQueue = new PriorityQueue<>(nodes.size(), new Comparator<Node>() {
		
			public int subt(Node h1, Node h2) {
				return h1.data - h2.data;
			}

			@Override
			public int compare(Node o1, Node o2) {
				// TODO Auto-generated method stub
				return 0;
			}
		});

		 for(Node node : nodes) {
		 	priorityQueue.add(node);
		 }
		 
		while(priorityQueue.size() > 1) {
			Node a = priorityQueue.poll();
			Node b = priorityQueue.poll();
			Node comb = new Node('_', a.data + b.data, a, b);
			priorityQueue.add(comb);
		}
		return priorityQueue.poll();
	}

	public static HashMap<Character, String> makeHash(Node t) {
		HashMap<Character, String> hashMap = new HashMap<>();
		hashHelp(t, "", hashMap);
		return hashMap;
	}

	public static void hashHelp(Node t, String f, HashMap<Character, String> hashMap) {
		if(t.l==null && t.r==null) {
			hashMap.put((char)t.data, f);
		} else {
			if (t.l != null) {
				hashHelp(t.l, f + "0", hashMap);
			}
			if (t.r != null) {
				hashHelp(t.r, f + "1", hashMap);
			}
		}
	}

	public static String makeCompress(int[] input, HashMap<Character, String> hashMap) {
		String output = "";
		for (int i = 0; i < input.length; i = i + 1) {
			output = output + hashMap.get(input[i]);
		}
		return output;
	}
	
	//
	public HuffmanTree(Scanner input) {
		
	}
	public void save(PrintStream output) {
		System.out.println(translate(root, "000100", 4));
		output.write(Integer.parseInt(translate(root, "000100", 4)));
	}

	public static String translate(Node input, String output, int setByte) {
		if(input==null) {
			return output;
		}
		else if(input.l==null && input.r==null) {
			output+="1";
			String add=Integer.toString(input.data, 2);
			System.out.println(input.data + " " + add);
			while(add.length()<setByte) {
				add = "0" + add;
			}
			output+=add;
		}
		else {
			output+="0";
			output = translate(input.l, output, setByte);
			output = translate(input.r, output, setByte);
		}
		return output;
	}
	
	private static class Node {
		 public int data;
		 public int frequency;
		 public Node l;
		 public Node r;
		 public Node(int a, int b, Node left, Node right){
			 data = a;
			 frequency = b;
			 l = left;
			 r = right;
		 }
		 public Node(int a, int b) {
			 data = a;
			 frequency = b;
			 l=null; r=null;
		 }
	 }
}
