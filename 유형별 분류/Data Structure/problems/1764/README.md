# <a href="https://www.acmicpc.net/problem/1764">1764 듣보잡</a>

<h3>문제</h3>
<ul>
  <li>김진영이 듣도 못한 사람의 명단과, 보도 못한 사람의 명단이 주어질 때, 듣도 보도 못한 사람의 명단을 구하는 프로그램을 작성하시오.</li>
  <li>입력
  <pre>
  첫째 줄에 듣도 못한 사람의 수 N, 보도 못한 사람의 수 M이 주어진다. 이어서 둘째 줄부터 N개의 줄에 걸쳐 듣도 못한 사람의 이름과, N+2째 줄부터 보도 못한 사람의 이름이 순서대로 주어진다. 이름은 띄어쓰기 없이 알파벳 소문자로만 이루어지며, 그 길이는 20 이하이다. N, M은 500,000 이하의 자연수이다. 듣도 못한 사람의 명단에는 중복되는 이름이 없으며, 보도 못한 사람의 명단도 마찬가지이다.
  </pre>
  </li>
  <li>출력
  <pre>
  듣보잡의 수와 그 명단을 사전순으로 출력한다.
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>ArrayList의 contains를 써도 동작에는 문제없으나 시간초과의 원인이 됨</li>
<li>같은 contains함수를 사용하지만 복잡도가 다름</li>
<li>ArrayList.contains() : O(n), HashSet.contains() : O(1)</li>
<li>ArrayList는 indexOf()를 사용하여 contain여부를 결정</li>
</ul>


<h3>풀이1(시간초과)</h3>
<pre>
<ul>
  <li><b>시간초과</b></li>
  <li>듣도 못한사람, 보도 못한 사람에서 공통으로 있는 사람을 찾아야함</li>
  <li>구분하지 않고 모두 입력받아 중복된 내용만 도출</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.List;

public class Main {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);

        List<String> namesList = new ArrayList<>();
        HashSet<String> namesSet = new HashSet<>();

        for (int i = 0; i < N + M; i++) {
            namesList.add(br.readLine());
        }

        for (String el : namesList) {
            if (namesList.indexOf(el) != namesList.lastIndexOf(el)) {
                namesSet.add(el);
            }
        }

        List<String> sortList = new ArrayList<>(namesSet);
        Collections.sort(sortList);
        for (String name : sortList) {
            bw.write(name + "\n");
        }

        bw.flush();
        bw.close();

    }
}

</code>
</pre>

<h3>풀이2(시간초과)</h3>
<pre>
<ul>
  <li><b>시간초과</b></li>
  <li>중복된 사람만 정렬하는 방식으로 바꿨음에도 시간초과</li>
  <li>중복 검사하는 과정에서 시간초과 의심</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.List;

public class Main {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);

        List<String> namesList = new ArrayList<>();
        List<String> namesTmp = new ArrayList<>();

        for (int i = 0; i < N; i++) {
			namesTmp.add(br.readLine());
		}

		for (int i = 0; i < M; i++) {
			String str = br.readLine();
			if (namesTmp.contains(str)) {
				namesList.add(str);
			}

		}

        Collections.sort(namesList);
        bw.write(namesList.size() + "\n");
        for(String name : namesList){
            bw.write(name + "\n");
        }
        bw.flush();
        bw.close();
    }
}

</code>
</pre>

<h3>풀이3(정답)</h3>
<pre>
<ul>
  <li>ArrayList로 입력받던것을 HashSet이용</li>
  <li>contains 속도 차이로 시간초과 해결</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.List;

public class Main {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);

        List<String> namesList = new ArrayList<>();
        HashSet<String> namesSet = new HashSet<>();

        for (int i = 0; i < N; i++) {
			namesSet.add(br.readLine());
		}

		for (int i = 0; i < M; i++) {
			String str = br.readLine();
			if (namesSet.contains(str)) {
				namesList.add(str);
			}

		}

        Collections.sort(namesList);
        bw.write(namesList.size() + "\n");
        for(String name : namesList){
            bw.write(name + "\n");
        }
        bw.flush();
        bw.close();
    }
}
</code>
</pre>
