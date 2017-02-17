package com.san.scribbles;

public class SortedSearch {

	static int counter = 0;

	public static void main(String[] args) {

		int[] sortedArray = new int[] { 1, 3, 5, 7, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25 };
		int lesserThan = 6;
		System.out.println(SortedSearch.countNumbers(sortedArray, lesserThan) + " items lesser than " + lesserThan
				+ " | Total Iterations:" + counter + " | Array size: " + sortedArray.length);

	}

	public static int countNumbers(int[] array, int lessThan) {

		return determineSubset(array, lessThan, array.length / 2, array.length);
	}

	private static int determineSubset(int[] array, int lessThan, int lastMaxIndex, int lastVisited) {
		counter++;
		if (lastMaxIndex == lastVisited) {
			return array[lastMaxIndex] < lessThan ? lastMaxIndex + 1 : lastMaxIndex;
		}

		if (array[lastMaxIndex] == lessThan) {
			return lastMaxIndex;
		} else if (array[lastMaxIndex] > lessThan) {
			int limit = 0;

			if (lastMaxIndex == 1) {
				limit = 0;
				lastMaxIndex = 0;
			} else {
				limit = lastMaxIndex - (int) (Math.ceil((lastMaxIndex) / 2));
			}
			lastMaxIndex = determineSubset(array, lessThan, limit, lastMaxIndex);

		} else {
			int limit = lastMaxIndex + (lastVisited - lastMaxIndex) / 2;
			lastMaxIndex = determineSubset(array, lessThan, limit, lastMaxIndex);
		}

		return lastMaxIndex;
	}
}
