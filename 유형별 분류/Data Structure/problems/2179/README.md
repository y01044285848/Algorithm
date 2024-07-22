# [2179 비슷한 단어](https://www.acmicpc.net/problem/2179)

<h3>문제</h3>
<ul>
  <li>
  N개의 영단어들이 주어졌을 때, 가장 비슷한 두 단어를 구해내는 프로그램을 작성하시오.

두 단어의 비슷한 정도는 두 단어의 접두사의 길이로 측정한다. 접두사란 두 단어의 앞부분에서 공통적으로 나타나는 부분문자열을 말한다. 즉, 두 단어의 앞에서부터 M개의 글자들이 같으면서 M이 최대인 경우를 구하는 것이다. "AHEHHEH", "AHAHEH"의 접두사는 "AH"가 되고, "AB", "CD"의 접두사는 ""(길이가 0)이 된다.

접두사의 길이가 최대인 경우가 여러 개일 때에는 입력되는 순서대로 제일 앞쪽에 있는 단어를 답으로 한다. 즉, 답으로 S라는 문자열과 T라는 문자열을 출력한다고 했을 때, 우선 S가 입력되는 순서대로 제일 앞쪽에 있는 단어인 경우를 출력하고, 그런 경우도 여러 개 있을 때에는 그 중에서 T가 입력되는 순서대로 제일 앞쪽에 있는 단어인 경우를 출력한다.
  </li>
  <li>입력
  <pre>
첫째 줄에 N(2 ≤ N ≤ 20,000)이 주어진다. 다음 N개의 줄에 알파벳 소문자로만 이루어진 길이 100자 이하의 서로 다른 영단어가 주어진다.
  </pre>
  </li>
  <li>출력
  <pre>
첫째 줄에 S를, 둘째 줄에 T를 출력한다. 단, 이 두 단어는 서로 달라야 한다. 즉, 가장 비슷한 두 단어를 구할 때 같은 단어는 제외하는 것이다.
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>자료구조 보단 문자열 다루기 문제?</li>
<li>입력받은 값은 중복되는 값은 없어야 하며, 순서를 가져야함</li>
<li>문자열을 문자 하나씩 비교하여 가장 많은 문자가 같은 문자열의 인덱스를 저장하여 마지막에 출력</li>
</ul>


<h3>풀이1(틀렸습니다)</h3>
<pre>
<ul>
<li>HashSet을 이용해 중복제거</li>
<li>문자열1, 문자열2를 순차적으로 반복하여 각 문자 비교</li>
<li>set은 순서를 가지지 않아 오류</li>
<li>set을 사용하기 위해서는 list로 입력 받은 후 set으로 변환 필요</li>
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
import java.util.Set;

public class Main {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int N = Integer.parseInt(br.readLine());
        Set<String> wordSet = new HashSet<>();
        for (int i = 0; i < N; i++) {
            wordSet.add(br.readLine());
        }

        ArrayList<String> words = new ArrayList<>(wordSet);

        int indexS = 0;
        int indexT = 0;
        int M = 0;

        for (int x = 0; x < N - 1; x++) {
            String word1 = words.get(x);
            for (int y = x+1; y < N; y++) {
                String word2 = words.get(y);
                int count = 0;
                for (int z = 0; z < Math.min(word1.length(), word2.length()); z++) {
                    if (word1.charAt(z) == word2.charAt(z)) {
                        count++;
                    } else {
                        break;
                    }
                }
                if (count > M) {
                    indexS = x;
                    indexT = y;
                    M = count;
                }
            }
        }
        bw.write(words.get(indexS) + "\n");
        bw.write(words.get(indexT));
        bw.flush();
        bw.close();
    }
}


</code>
</pre>

<h3>풀이2(정답)</h3>
<pre>
<ul>
<li>위와 같은 방식으로 풀이</li>
<li>ArrayList로 입력받고 입력받을때 문자열이 있는지 검사 후 저장</li>
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
import java.util.Iterator;
import java.util.List;
import java.util.Set;

public class Main {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int N = Integer.parseInt(br.readLine());

        ArrayList<String> words = new ArrayList<>();
        for (int i = 0; i < N; i++) {
            String s = br.readLine();
            if (!words.contains(s)) {
                words.add(s);
            }
        }

        int indexS = 0;
        int indexT = 0;
        int M = 0;

        for (int x = 0; x < N - 1; x++) {
            String word1 = words.get(x);
            for (int y = x + 1; y < N; y++) {
                String word2 = words.get(y);
                int count = 0;
                for (int z = 0; z < Math.min(word1.length(), word2.length()); z++) {
                    if (word1.charAt(z) == word2.charAt(z)) {
                        count++;
                    } else {
                        break;
                    }
                }
                if (count > M) {
                    indexS = x;
                    indexT = y;
                    M = count;
                }
            }
        }
        bw.write(words.get(indexS) + "\n");
        bw.write(words.get(indexT));
        bw.flush();
        bw.close();
    }
}

</code>
</pre>

</code>
</pre>