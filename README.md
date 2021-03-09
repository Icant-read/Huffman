# Huffman
package binaryTrees;
import java.io.File;
import java.io.FileWriter;
import java.io.PrintStream;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.Scanner;
import java.util.TreeMap;


public class HuffmanTree {

	private Node root;
	
	public HuffmanTree(int[] frequencies) {
		Queue q = new PriorityQueue();
	}
	public HuffmanTree(Scanner input) {
		
	}

	public void save(PrintStream output) {
		System.out.println(translate(root, ""));
		output.write(Integer.parseInt(translate(root, "")));
	}
	public String translate(Node input, String output) {
		if(input==null) {
			return output;
		}
		else if(input.l==null && input.r==null) {
			output+="1";
			output+=input.data;
		}
		else {
			output = translate(input.l, output);
			output+="0";
			String add=Integer.toString(input.data, 2);
			while(add.length()<4) {
				add = "0" + add;
			}
			output = translate(input.r, output);
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
