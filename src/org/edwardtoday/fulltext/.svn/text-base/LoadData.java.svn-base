package org.edwardtoday.fulltext;

import java.io.*;
import java.util.*;

/**
 * @author edwardtoday
 * 
 */
public class LoadData {

	static int currentDocID = 0;
	static int currentSynonymID = 0;
	static HashMap<String, Integer> idf = new HashMap<String, Integer>();
	static ArrayList<IndexNode> index = new ArrayList<IndexNode>();
	static HashMap<Character, HashSet<Integer>> invlist = new HashMap<Character, HashSet<Integer>>();
	static HashMap<String, HashSet<Integer>> invWordList = new HashMap<String, HashSet<Integer>>();
	static String query = "";
	static String searchPath = "./Data";
	static ArrayList<ResultNode> searchResults = new ArrayList<ResultNode>();
	static HashSet<String> stoplist = new HashSet<String>();
	static String stoplistPath = "./misc/stoplist.txt";
	static HashMap<Integer, HashSet<String>> synonymDict = new HashMap<Integer, HashSet<String>>();
	static HashMap<String, Integer> synonymIndex = new HashMap<String, Integer>();
	static String synonymsPath = "./misc/synonymlist.txt";
	static double wordResults = 0, charResults = 0, wordSearchTime = 0,
			indexedSearchTime = 0;

	/**
	 * clear search results
	 */
	public static void clear() {
		LoadData.searchResults.clear();
		System.gc();
	}

	/**
	 * @throws IOException
	 */
	public static void init() throws IOException {
		LoadData.index.clear();
		LoadData.invlist.clear();
		LoadData.currentDocID = 0;
		double startAll = 0, start = 0;
		double endAll = 0, end = 0;
		System.gc();
		startAll = Runtime.getRuntime().totalMemory();
		start = Runtime.getRuntime().freeMemory();

		// read text files
		long starttime = System.nanoTime();
		System.out.println("Loading stoplist...");
		LoadData.loadStopList(new File(LoadData.stoplistPath));
		System.out.println(LoadData.stoplist.size() + " words loaded.");
		System.out.println("Loading synonyms...");
		LoadData.loadSynonymsList(new File(LoadData.synonymsPath));
		System.out.println(LoadData.synonymDict.size() + " lines loaded.");
		System.out.println("Reading text files.");
		LoadData.recursiveReadDir(new File(LoadData.searchPath));
		long endtime = System.nanoTime();
		LoadData.wordSearchTime = endtime - starttime;
		System.out.println("File loading time: " + LoadData.wordSearchTime);
		System.gc();
		System.out.println("# of files processed: "
				+ (LoadData.currentDocID - 1));
		endAll = Runtime.getRuntime().totalMemory();
		end = Runtime.getRuntime().freeMemory();
		LoadData.wordResults = ((endAll - end) - (startAll - start)) / 1024;

		// create inverted index
		System.out.println("Creating index.");
		starttime = System.nanoTime();
		LoadData.createInvertedIndex();
		LoadData.createInvertedWordIndex();
		endtime = System.nanoTime();
		LoadData.indexedSearchTime = endtime - starttime;
		System.out
				.println("Index creation time: " + LoadData.indexedSearchTime);
		System.gc();
		System.out.println("# of index entries: " + LoadData.invlist.size());
		endAll = Runtime.getRuntime().totalMemory();
		end = Runtime.getRuntime().freeMemory();
		LoadData.charResults = ((endAll - end) - (startAll - start)) / 1024;

	}

	static void createInvertedIndex() {
		for (final IndexNode curDoc : LoadData.index) {
			for (final Character curCh : curDoc.docContent) {
				if (!LoadData.invlist.containsKey(curCh)) {
					final HashSet<Integer> docs = new HashSet<Integer>();
					docs.add(curDoc.docID);
					LoadData.invlist.put(curCh, docs);
				} else {
					final HashSet<Integer> docs = LoadData.invlist.get(curCh);
					docs.add(curDoc.docID);
					LoadData.invlist.remove(curCh);
					LoadData.invlist.put(curCh, docs);
				}
			}
		}
	}

	static void createInvertedWordIndex() {
		for (final IndexNode curDoc : LoadData.index) {
			for (final String curWord : curDoc.docWords) {
				if (!LoadData.invWordList.containsKey(curWord)) {
					final HashSet<Integer> docs = new HashSet<Integer>();
					docs.add(curDoc.docID);
					LoadData.invWordList.put(curWord, docs);
				} else {
					final HashSet<Integer> docs = LoadData.invWordList
							.get(curWord);
					docs.add(curDoc.docID);
					LoadData.invWordList.remove(curWord);
					LoadData.invWordList.put(curWord, docs);
				}
				// proc tf
				if (curDoc.tf.containsKey(curWord)) {
					final int tmptf = curDoc.tf.get(curWord) + 1;
					curDoc.tf.remove(curWord);
					curDoc.tf.put(curWord, tmptf);
				} else {
					curDoc.tf.put(curWord, 1);
				}
			}
			// proc idf
			for (final Object element : curDoc.tf.keySet()) {
				final String key = (String) element;
				if (LoadData.idf.containsKey(key)) {
					final int tmpidf = LoadData.idf.get(key) + 1;
					LoadData.idf.remove(key);
					LoadData.idf.put(key, tmpidf);
				} else {
					LoadData.idf.put(key, 1);
				}
			}
		}
	}

	static ArrayList<String> genResultIDList(final ArrayList<ResultNode> result) {
		final ArrayList<String> resultList = new ArrayList<String>();
		for (final ResultNode rn : result) {
			final String tmp = Integer.toString(rn.docID) + " : "
					+ Double.toString(rn.tfidf);
			resultList.add(tmp);
		}
		return resultList;
	}

	/**
	 * @return currentDocID
	 */
	static final int getCurrentDocID() {
		return LoadData.currentDocID++;
	}

	/**
	 * @return currentSynonymID
	 */
	static final int getCurrentSynonymID() {
		return LoadData.currentSynonymID++;
	}

	static String getDocPreview(final int resultIdx) {
		final int pos2 = LoadData.min(LoadData.index.get(LoadData.searchResults
				.get(resultIdx).docID).docContent.size() - 1, 100);
		return LoadData.index.get(LoadData.searchResults.get(resultIdx).docID).docString
				.substring(0, pos2);
	}

	static String getDocURI(final int resultIdx) {
		return LoadData.index.get(LoadData.searchResults.get(resultIdx).docID).docURI
				.toString();
	}

	static ArrayList<ResultNode> indexSearch(final String query) {
		if (query.length() == 0)
			return new ArrayList<ResultNode>();

		LoadData.indexedSearchTime = 0;
		long timer1, timer2;
		final char[] charQuery = query.toCharArray();
		// query splitter
		timer1 = System.nanoTime();
		final ArrayList<Character> c = new ArrayList<Character>();
		for (final char ch : charQuery) {
			if (ch != ' ') {
				c.add(ch);
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tQuery splitter time: " + (timer2 - timer1));
		LoadData.indexedSearchTime += timer2 - timer1;

		// get the shortest one of query results
		boolean found = true;
		timer1 = System.nanoTime();
		HashSet<Integer> shortest = LoadData.invlist.get(c.get(0));
		for (final Character ch : c) {
			if (!LoadData.invlist.containsKey(ch)) {
				found = false;
				break;
			} else {
				final HashSet<Integer> curSet = LoadData.invlist.get(ch);
				if (shortest.size() > curSet.size()) {
					shortest = curSet;
				}
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tFinding shortest time: " + (timer2 - timer1));
		LoadData.indexedSearchTime += timer2 - timer1;

		// calc the intersection of all query results
		// new algo
		timer1 = System.nanoTime();
		final ArrayList<ResultNode> result = new ArrayList<ResultNode>();
		if (found) {
			for (final Character ch : c) {
				final HashSet<Integer> tmp = LoadData.invlist.get(ch);
				shortest.retainAll(tmp);
			}
			for (final Integer cid : shortest) {
				result.add(new ResultNode(cid));
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tIntersection time: " + (timer2 - timer1)
				+ " with " + result.size() + " results");
		LoadData.indexedSearchTime += timer2 - timer1;
		System.out.println("Char index search time: "
				+ LoadData.indexedSearchTime);

		return result;
	}

	static ArrayList<ResultNode> linearSearch(final String query) {
		LoadData.wordSearchTime = 0;

		long timer1, timer2;
		final char[] charQuery = query.toCharArray();
		// query splitter
		timer1 = System.nanoTime();
		final ArrayList<Character> c = new ArrayList<Character>();
		for (final char ch : charQuery) {
			if (ch != ' ') {
				c.add(ch);
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tQuery splitter time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;

		final ArrayList<ResultNode> result = new ArrayList<ResultNode>();

		timer1 = System.nanoTime();
		for (final IndexNode curDoc : LoadData.index) {
			if (curDoc.docContent.containsAll(c)) {
				final ResultNode curRes = new ResultNode();
				curRes.docID = curDoc.docID;
				for (final Character ch : c) {
					curRes.pos.add(curDoc.docString.indexOf(ch));
				}
				result.add(curRes);
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tLooking up time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;
		System.out.println("Linear search time: " + LoadData.wordSearchTime);

		return result;
	}

	static void loadStopList(final File file) throws IOException {
		String line;

		final InputStreamReader isr = new InputStreamReader(
				new FileInputStream(file), "GBK");
		final BufferedReader reader = new BufferedReader(isr);
		while ((line = reader.readLine()) != null) {
			LoadData.stoplist.add(line);
		}
	}

	static void loadSynonymsList(final File file) throws IOException {
		String line;

		final InputStreamReader isr = new InputStreamReader(
				new FileInputStream(file), "GBK");
		final BufferedReader reader = new BufferedReader(isr);
		while ((line = reader.readLine()) != null) {
			final int curID = LoadData.getCurrentSynonymID();
			final StringTokenizer st = new StringTokenizer(line);
			while (st.hasMoreTokens()) {
				final String newWord = st.nextToken();
				LoadData.synonymIndex.put(newWord, curID);
				if (!LoadData.synonymDict.containsKey(curID)) {
					final HashSet<String> pairs = new HashSet<String>();
					pairs.add(newWord);
					LoadData.synonymDict.put(curID, pairs);
				} else {
					final HashSet<String> pairs = LoadData.synonymDict
							.get(curID);
					pairs.add(newWord);
					LoadData.synonymDict.remove(curID);
					LoadData.synonymDict.put(curID, pairs);
				}
			}
		}
	}

	static int max(final int a, final int b) {
		if (a > b)
			return a;
		return b;
	}

	static int min(final int a, final int b) {
		if (a > b)
			return b;
		return a;
	}

	static void recursiveReadDir(final File file) throws IOException {
		final IndexNode temp = new IndexNode();
		if (!file.isDirectory()) {
			temp.docID = LoadData.getCurrentDocID();
			temp.docURI = file.toURI();

			String line;

			final InputStreamReader isr = new InputStreamReader(
					new FileInputStream(file), "GBK");
			final BufferedReader reader = new BufferedReader(isr);
			while ((line = reader.readLine()) != null) {
				final StringTokenizer st = new StringTokenizer(line);
				while (st.hasMoreTokens()) {
					final StringTokenizer st2 = new StringTokenizer(st
							.nextToken(), "/");
					final String newWord = st2.nextToken();
					final char[] chars = newWord.toCharArray();
					temp.wordCount++;
					temp.docString += newWord; // full-text
					if (!LoadData.stoplist.contains(newWord)) {
						temp.docWords.add(newWord); // word index
					}
					for (final char newChar : chars) {
						temp.docContent.add(newChar); // char index
					}
				}
			}
			LoadData.index.add(temp);

		} else {
			final File[] files = file.listFiles();
			for (final File file2 : files) {
				LoadData.recursiveReadDir(file2);
			}
		}
	}

	static ArrayList<ResultNode> wordIndexSearch(final HashSet<String> querys) {
		if (querys.size() == 0)
			return new ArrayList<ResultNode>();
		long timer1, timer2;
		// final ArrayList<String> querys = new ArrayList<String>(); // query
		// words

		// get the shortest one of query results
		boolean found = true;
		timer1 = System.nanoTime();
		boolean first = true;
		HashSet<Integer> shortest = new HashSet<Integer>();
		for (final String word : querys) {
			if (!LoadData.invWordList.containsKey(word)) {
				found = false;
				break;
			} else {
				final HashSet<Integer> curSet = LoadData.invWordList.get(word);
				if (first) {
					shortest = curSet;
					first = false;
				} else if (shortest.size() > curSet.size()) {
					shortest = curSet;
				}
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tFinding shortest time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;

		// calc the intersection of all query results
		// new algo
		timer1 = System.nanoTime();
		final ArrayList<ResultNode> result = new ArrayList<ResultNode>();
		if (found) {
			for (final String word : querys) {
				final HashSet<Integer> tmp = LoadData.invWordList.get(word);
				shortest.retainAll(tmp);
			}
			for (final Integer cid : shortest) {
				result.add(new ResultNode(cid));
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tIntersection time: " + (timer2 - timer1)
				+ " with " + result.size() + " results");
		LoadData.wordSearchTime += timer2 - timer1;
		System.out
				.println("Word index search time: " + LoadData.wordSearchTime);

		return result;
	}

	static ArrayList<ResultNode> wordIndexSearchTFIDF(final String query) {
		long timer1, timer2;
		LoadData.wordSearchTime = 0;
		timer1 = System.nanoTime();
		final HashSet<String> querys = new HashSet<String>(); // query words
		final StringTokenizer st = new StringTokenizer(query);
		while (st.hasMoreTokens()) {
			final String nextQuery = st.nextToken();
			if (stoplist.contains(nextQuery))
				continue;
			if (!LoadData.synonymIndex.containsKey(nextQuery)) {
				querys.add(nextQuery);
			} else {
				final HashSet<String> pairs = LoadData.synonymDict
						.get(LoadData.synonymIndex.get(nextQuery));
				final Iterator itr = pairs.iterator();
				while (itr.hasNext()) {
					final String nextQuerySynonym = (String) itr.next();
					querys.add(nextQuerySynonym);
				}
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tQuery splitter time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;

		System.out.print("Ready to search: ");
		final Iterator querysIterator = querys.iterator();
		while (querysIterator.hasNext()) {
			System.out.print((String) querysIterator.next() + " ");
		}
		System.out.print("\n");

		final ArrayList<ResultNode> normalResult = LoadData
				.wordIndexSearch(querys);

		// calc tf*idf
		timer1 = System.nanoTime();
		for (final ResultNode rn : normalResult) {
			for (final String term : querys) {
				final double tf1 = LoadData.index.get(rn.docID).tf.get(term);
				final double tf2 = LoadData.index.get(rn.docID).wordCount;
				final double curtf = Math.log(1 + tf1 / tf2);
				final double idf1 = (LoadData.currentDocID - 1);
				final double idf2 = (LoadData.idf.get(term));
				final double curidf = Math.log(idf1 / idf2);
				final double curtfidf = curtf * curidf;
				rn.tfidf *= curtfidf;
			}
		}
		timer2 = System.nanoTime();
		System.out.println("\tTF*IDF calc time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;
		// sort results
		timer1 = System.nanoTime();
		final ResultNodeComparator rnc = new ResultNodeComparator();
		Collections.sort(normalResult, rnc);
		timer2 = System.nanoTime();
		System.out.println("\tResult sort time: " + (timer2 - timer1));
		LoadData.wordSearchTime += timer2 - timer1;
		return normalResult;
	}
}

class ResultNodeComparator implements Comparator<ResultNode> {

	public int compare(final ResultNode aNode, final ResultNode bNode) {
		final double comp = aNode.tfidf - bNode.tfidf;
		if (comp > 0)
			return -1;
		else if (comp < 0)
			return 1;
		else
			return 0;
	}
}
