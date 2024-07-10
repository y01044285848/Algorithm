# [13164 행복 유치원](https://www.acmicpc.net/problem/13164)

<h3>문제</h3>
<ul>
  <li>행복 유치원 원장인 태양이는 어느 날 N명의 원생들을 키 순서대로 일렬로 줄 세우고, 총 K개의 조로 나누려고 한다. 각 조에는 원생이 적어도 한 명 있어야 하며, 같은 조에 속한 원생들은 서로 인접해 있어야 한다. 조별로 인원수가 같을 필요는 없다.

이렇게 나뉜 조들은 각자 단체 티셔츠를 맞추려고 한다. 조마다 티셔츠를 맞추는 비용은 조에서 가장 키가 큰 원생과 가장 키가 작은 원생의 키 차이만큼 든다. 최대한 비용을 아끼고 싶어 하는 태양이는 K개의 조에 대해 티셔츠 만드는 비용의 합을 최소로 하고 싶어 한다. 태양이를 도와 최소의 비용을 구하자.</li>
<li>입력
  <pre>
입력의 첫 줄에는 유치원에 있는 원생의 수를 나타내는 자연수 N(1 ≤ N ≤ 300,000)과 나누려고 하는 조의 개수를 나타내는 자연수 K(1 ≤ K ≤ N)가 공백으로 구분되어 주어진다. 다음 줄에는 원생들의 키를 나타내는 N개의 자연수가 공백으로 구분되어 줄 서 있는 순서대로 주어진다. 태양이는 원생들을 키 순서대로 줄 세웠으므로, 왼쪽에 있는 원생이 오른쪽에 있는 원생보다 크지 않다. 원생의 키는 109를 넘지 않는 자연수이다.
  </pre>
  </li>
<li>출력
  <pre>
  티셔츠 만드는 비용이 최소가 되도록 K개의 조로 나누었을 때, 티셔츠 만드는 비용을 출력한다.
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>N(총인원), K(조 개수)가 정해졌을 때, (N - K)번 조편성을 하면 됨</li>
<li>앞사람과의 키 차이가 작은 순서로 조편성</li>
</ul>


<h3>풀이(정답)</h3>
<ul>
  <li>입력받는 수열은 정렬되어 있음</li>
  <li>입력받은 값을 리스트로 저장하여 인덱스1부터 앞의 값과 차이를 저장하는 리스트 생성</li>
  <li>차이값을 가지고 있는 리스트를 정렬하여 N-K개수 만큼 더함</li>
</ul>
<pre>
<code>
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String nk = br.readLine();
        int N = Integer.parseInt(nk.split(" ")[0]);
        int K = Integer.parseInt(nk.split(" ")[1]);

        List<Integer> numList = new ArrayList<>();
        String nums = br.readLine();
        for (String num : nums.split(" ")) {
            numList.add(Integer.valueOf(num));
        }

        List<Integer> diff = new ArrayList<>();
        for(int i = 1; i < N; i++){
            diff.add(numList.get(i) - numList.get(i - 1));
        }
        Collections.sort(diff);

        int result = 0;
        for(int j = 0; j < N - K; j++){
            result += diff.get(j);
        }
        System.out.println(result);
    }
}
</code>
</pre>
