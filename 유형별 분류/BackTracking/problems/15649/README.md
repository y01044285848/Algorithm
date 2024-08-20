# [15649 N과 M(1)](https://www.acmicpc.net/problem/15649)

<h3>문제</h3>
<ul>
  <li>자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열</li>
<li>입력
  <pre>
첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)
  </pre>
  </li>
<li>출력
  <pre>
  한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.

수열은 사전 순으로 증가하는 순서로 출력해야 한다.
  </pre>
  </li>
</ul>

<h3>개념</h3>
<ul>
<li>노드의 '유망성'을 판단한 뒤, 해당 노드가 유망하지 않다면 부모 노드로 돌아가 다른 자식 노드를 찾는 방법</li>
<li>브루트포스, 백트래킹, DFS 정리</li>
<pre>
" a + b + c + d = 20 을 만족하는 두 수를 모두 찾아내시오. ( 0 ≤ a ,b ,c ,d < 100) "

 
이 때 브루트포스는 말 그대로 '모든 경우의 수'를 찾아보는 것이다. 

즉, a = 1, b = 1, c =1, d = 1 부터 시작하여 a = 100, b = 100, c = 100, d = 100 까지 총 1억개의 경우의 수를 모두 찾아보면서 a + b + c + d = 20 이 만족하는 값을 탐색하는 것이다. 브루트포스가 강력한 점은 모든 경우의 수를 탐색하다보니 만족하는 값을 100% 찾아낸다는 점이다. 반대로 단점이라면 모든 경우의 수를 판단하는 만큼 조합 가능한 경우의 수가 많으면 많을 수록 자원을 매우 많이 필요로 한다는 점이다.

 

백트래킹은 앞서 말했듯이 해당 노드의 유망성을 판단한다고 했다. 이 말은 즉 해당 범위 내에서 조건을 추가하여 값의 유망성을 판단한다는 의미이다. 하나라도 a = 21 또는 b = 21 또는 c = 21 또는 d = 21 일 경우 20일 가능성이 1 ~ 100 범위 내에서는 절대 불가능하다. 그렇기 때문에 a > 20 이거나 b > 20, c > 20, d > 20 일 경우는 탐색하지 않는다. 그렇게 된다면 탐색하는데 필요한 자원을 많이 줄일 수 있다.

 

DFS(깊이우선탐색)은 트리순회의 한 형태다. 하나의 순회 알고리즘으로 백트래킹에 사용하는 대표적인 탐색 알고리즘이다. 즉, 백트래킹 = DFS가 아니라 백트래킹의 방법 중 하나가 DFS인 것이다. 그 외에도 BFS(너비우선탐색) 등 다양한 방법으로 백트래킹을 구현할 수 있다. 
</pre>
</ul>


<h3>풀이(정답)</h3>
<ul>
  <li>출력이 필요한 명령(조회 필요 명령)은 비어있는지 확인</li>
  <li>값을 넣는 명령은 출력없음</li>
</ul>
<pre>
<code>
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;
 
public class Main {
 
	public static int[] arr;
	public static boolean[] visit;
	public static StringBuilder sb = new StringBuilder();
 
	public static void main(String[] args) throws IOException {
 
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
 
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
 
		arr = new int[M];
		visit = new boolean[N];
		dfs(N, M, 0);
		System.out.println(sb);
 
	}
 
	public static void dfs(int N, int M, int depth) {
		if (depth == M) {
			for (int val : arr) {
				sb.append(val).append(' ');
			}
			sb.append('\n');
			return;
		}
 
		for (int i = 0; i < N; i++) {
			if (!visit[i]) {
				visit[i] = true;
				arr[depth] = i + 1;
				dfs(N, M, depth + 1);
				visit[i] = false;
			}
		}
	}
 
}
</code>
</pre>
