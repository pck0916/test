import java.util.*;
public class Main {
	static int[][] maze;
	static int n;
	static int min;
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		min = n*n;
		maze = new int[n][n];
		for(int i=0;i<n;i++)
			for(int j=0;j<n;j++) 
				maze[i][j] = sc.nextInt();
		recursion(1, 1, 0);
		if(min==n*n)
			System.out.println("No solution");
		else 
			System.out.println(min);
	}
	public static void recursion(int x, int y, int count) {
		if(x==n-2 && y==n-2)
			min = Math.min(count, min);
		else {
			maze[x][y]=1;							//锁定，防止在递归的过程中再次递归已经访问过的结点导致无限循环
			if(y<n-1 && maze[x][y+1]==0) {
				recursion(x, y+1, count+1);			//右
			}
			if(x<n-1 && maze[x+1][y]==0) {
				recursion(x+1, y, count+1);			//下
			}
			if(x>1 && maze[x-1][y]==0) {
				recursion(x-1, y, count+1);			//上
			}
			if(y>1 && maze[x][y-1]==0) {
				recursion(x, y-1, count+1);			//左
			}
			maze[x][y]=0;							//当这个节点往后的节点已经都递归过了，则解除锁定
													//防止有其他路径也需要走这个节点但是已经不通
		}
	}
}
