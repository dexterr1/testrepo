# NQUEEN 

public class NQueenProblem {
	final int N = 4;

	void printSolution(int board[][])
	{
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < N; j++)
				System.out.print(" " + board[i][j]
								+ " ");
			System.out.println();
		}
	}

	boolean isSafe(int board[][], int row, int col)
	{
		int i, j;

		
		for (i = 0; i < col; i++)
			if (board[row][i] == 1)
				return false;

		for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
			if (board[i][j] == 1)
				return false;


		for (i = row, j = col; j >= 0 && i < N; i++, j--)
			if (board[i][j] == 1)
				return false;

		return true;
	}

	boolean solveNQUtil(int board[][], int col)
	{

		if (col >= N)
			return true;

		for (int i = 0; i < N; i++) {
			if (isSafe(board, i, col)) {
		
				board[i][col] = 1;

			
				if (solveNQUtil(board, col + 1) == true)
					return true;


				board[i][col] = 0; // BACKTRACK
			}
		}
		return false;
	}


	boolean solveNQ()
	{
		int board[][] = { { 0, 0, 0, 0 },
						{ 0, 0, 0, 0 },
						{ 0, 0, 0, 0 },
						{ 0, 0, 0, 0 } };

		if (solveNQUtil(board, 0) == false) {
			System.out.print("Solution does not exist");
			return false;
		}

		printSolution(board);
		return true;
	}


	public static void main(String args[])
	{
		NQueenProblem Queen = new NQueenProblem();
		Queen.solveNQ();
	}
}


#knapsack python 

# A naive recursive implementation
# of 0-1 Knapsack Problem

# Returns the maximum value that
# can be put in a knapsack of
# capacity W


def knapSack(W, wt, val, n):

	if n == 0 or W == 0:
		return 0

	if (wt[n-1] > W):
		return knapSack(W, wt, val, n-1)


	else:
		return max(
			val[n-1] + knapSack(
				W-wt[n-1], wt, val, n-1),
			knapSack(W, wt, val, n-1))




#Driver Code
val = [60, 100, 120]
wt = [10, 20, 30]
W = 50
n = len(val)
print knapSack(W, wt, val, n)


#job sequencing 
# Program to find the maximum profit
# job sequence from a given array
# of jobs with deadlines and profits

# function to schedule the jobs take 2
# arguments array and no of jobs to schedule


def printJobScheduling(arr, t):

	# length of array
	n = len(arr)

	for i in range(n):
		for j in range(n - 1 - i):
			if arr[j][2] < arr[j + 1][2]:
				arr[j], arr[j + 1] = arr[j + 1], arr[j]

	# To keep track of free time slots
	result = [False] * t


	job = ['-1'] * t

	
	for i in range(len(arr)):

		for j in range(min(t - 1, arr[i][1] - 1), -1, -1):

			# Free slot found
			if result[j] is False:
				result[j] = True
				job[j] = arr[i][0]
				break


	print(job)


# Driver COde
arr = [['a', 2, 100], # Job Array
	['b', 1, 19],
	['c', 2, 27],
	['d', 1, 25],
	['e', 3, 15]]


print("Following is maximum profit sequence of jobs")


printJobScheduling(arr, 3)





