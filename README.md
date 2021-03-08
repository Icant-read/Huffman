# Huffman
package binaryTrees;

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
		
	}
	public <BitInputStream> void translate(BitInputStream input, PrintStream output) {
		
	}
	
	private static class Node {
		 int data;
		 Node l;
		 Node r;
		 public Node(int a, Node left, Node right){
			 data = a;
			 l = left;
			 r = right;
		 }
		 public Node(int a) {
			 data = a;
			 l=null; r=null;
		 }
	 }
}
