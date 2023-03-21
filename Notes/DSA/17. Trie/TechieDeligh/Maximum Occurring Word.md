**Problem:**
Given a set of strings with duplicates present, return the maximum occurring word in it. If two words have the same count, return any one of them.

**Example:**

	Input: [code, coder, coding, codable, codec, codecs, coded, codeless, codecs, codependence,
				 codex, codify, codependents, codes, code, coder, codesign, codec, codeveloper, 
				 codrive, codec, codecs, codiscovered]
	Output: codec or codecs


```java

class Solution
{
	public static String lexicographicSort(List<String> words)
	{
		Trie trie = new Trie();
		for(String word : words){
			trie.insert(word);
		}
		
		return trie.mostFrequent;
	}
	
	static class Trie{
		TrieNode root = new TrieNode();
		String mostFrequent = null;
		int maxEndCount = 0;
		public void insert(String word){
			TrieNode current = root;
			for(char ch : word.toCharArray()){
				if(current.edges[ch-'a']==null)
					current.edges[ch - 'a'] = new TrieNode();
				current = current.edges[ch-'a'];
			}
			
			current.endCount++;
			if(maxEndCount < current.endCount) {
				maxEndCount = current.endCount;
				mostFrequent = word;
			}
		}
		
		private class TrieNode{
			TrieNode[] edges = new TrieNode[26];
			int endCount = 0;
		}
	}
}

```