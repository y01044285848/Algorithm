# [24511 queuestack](https://www.acmicpc.net/problem/24511)

<h3>문제</h3>
<ul>
  <li>한가롭게 방학에 놀고 있던 도현이는 갑자기 재밌는 자료구조를 생각해냈다. 그 자료구조의 이름은 queuestack이다.

queuestack의 구조는 다음과 같다. 
1번, 
2번, ... , 
N번의 자료구조(queue 혹은 stack)가 나열되어있으며, 각각의 자료구조에는 한 개의 원소가 들어있다.

queuestack의 작동은 다음과 같다.

 
x_0을 입력받는다.
 
x_0을 
1번 자료구조에 삽입한 뒤 
1번 자료구조에서 원소를 pop한다. 그때 pop된 원소를 
x_1이라 한다.
 
x_1을 
2번 자료구조에 삽입한 뒤 
2번 자료구조에서 원소를 pop한다. 그때 pop된 원소를 
x_2이라 한다.
...
 
x_{N-1}을 
N번 자료구조에 삽입한 뒤 
N번 자료구조에서 원소를 pop한다. 그때 pop된 원소를 
x_N이라 한다.
 
x_N을 리턴한다.
도현이는 길이 
M의 수열 
C를 가져와서 수열의 원소를 앞에서부터 차례대로 queuestack에 삽입할 것이다. 이전에 삽입한 결과는 남아 있다. (예제 1 참고)

queuestack에 넣을 원소들이 주어졌을 때, 해당 원소를 넣은 리턴값을 출력하는 프로그램을 작성해보자.</li>
<li>입력
  <pre>
첫째 줄에 queuestack을 구성하는 자료구조의 개수 
N이 주어진다. (1 ≤ N ≤ 100,000)

둘째 줄에 길이 
N의 수열 
A가 주어진다. 
i번 자료구조가 큐라면 
A_i = 0, 스택이라면 
A_i = 1이다.

셋째 줄에 길이 
N의 수열 
B가 주어진다. 
B_i는 
i번 자료구조에 들어 있는 원소이다. (1 ≤ B_i ≤ 1,000,000,000)

넷째 줄에 삽입할 수열의 길이 
$M$이 주어진다. (
$1 ≤ M ≤ 100,000)

다섯째 줄에 queuestack에 삽입할 원소를 담고 있는 길이 
M의 수열 
C가 주어진다. (1 ≤ C_i ≤ 1,000,000,000)

입력으로 주어지는 모든 수는 정수이다.
  </pre>
  </li>
<li>출력
  <pre>
  수열 
C의 원소를 차례대로 queuestack에 삽입했을 때의 리턴값을 공백으로 구분하여 출력한다.
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>queuestack이지만 큐만 활용</li>
<li>스택은 값에 영향을 주지 않기 때문에 제외하고 생각</li>
</ul>


<h3>풀이(정답)</h3>
<ul>
  <li>스택은 값에 영향을 미치지 않기 때문에 1의 값은 제외하고 생각</li>
  <li>선입선출인 큐에 값을 넣는다 생각하여 구현</li>
</ul>
<pre>
<code>
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];
        Deque<Integer> deque = new ArrayDeque<>();

        StringTokenizer st = new StringTokenizer(br.readLine());
        for(int i=0; i<N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        st = new StringTokenizer(br.readLine());
        for(int i=0; i<N; i++) {
            int num = Integer.parseInt(st.nextToken());
            if (arr[i] == 0)
                deque.addLast(num);
        }

        int M = Integer.parseInt(br.readLine());
        st = new StringTokenizer(br.readLine());
        
        StringBuilder sb = new StringBuilder();
        for(int i=0; i<M; i++) {
            deque.addFirst(Integer.parseInt(st.nextToken()));
            sb.append(deque.pollLast()).append(" ");
        }
        System.out.println(sb);
    }
}

</code>
</pre>
