# [1620 나는야 포켓몬 마스터 이다솜](https://www.acmicpc.net/problem/1620)

<h3>문제</h3>
<ul>
  <li>오박사 : 그럼 다솜아 이제 진정한 포켓몬 마스터가 되기 위해 도감을 완성시키도록 하여라. 일단 네가 현재 가지고 있는 포켓몬 도감에서 포켓몬의 이름을 보면 포켓몬의 번호를 말하거나, 포켓몬의 번호를 보면 포켓몬의 이름을 말하는 연습을 하도록 하여라. 나의 시험을 통과하면, 내가 새로 만든 도감을 주도록 하겠네.</li>
  <li>입력
  <pre>
첫째 줄에는 도감에 수록되어 있는 포켓몬의 개수 N이랑 내가 맞춰야 하는 문제의 개수 M이 주어져. N과 M은 1보다 크거나 같고, 100,000보다 작거나 같은 자연수인데, 자연수가 뭔지는 알지? 모르면 물어봐도 괜찮아. 나는 언제든지 질문에 답해줄 준비가 되어있어.

둘째 줄부터 N개의 줄에 포켓몬의 번호가 1번인 포켓몬부터 N번에 해당하는 포켓몬까지 한 줄에 하나씩 입력으로 들어와. 포켓몬의 이름은 모두 영어로만 이루어져있고, 또, 음... 첫 글자만 대문자이고, 나머지 문자는 소문자로만 이루어져 있어. 아참! 일부 포켓몬은 마지막 문자만 대문자일 수도 있어. 포켓몬 이름의 최대 길이는 20, 최소 길이는 2야. 그 다음 줄부터 총 M개의 줄에 내가 맞춰야하는 문제가 입력으로 들어와. 문제가 알파벳으로만 들어오면 포켓몬 번호를 말해야 하고, 숫자로만 들어오면, 포켓몬 번호에 해당하는 문자를 출력해야해. 입력으로 들어오는 숫자는 반드시 1보다 크거나 같고, N보다 작거나 같고, 입력으로 들어오는 문자는 반드시 도감에 있는 포켓몬의 이름만 주어져.
  </pre>
  </li>
  <li>출력
  <pre>
첫째 줄부터 차례대로 M개의 줄에 각각의 문제에 대한 답을 말해줬으면 좋겠어!!!. 입력으로 숫자가 들어왔다면 그 숫자에 해당하는 포켓몬의 이름을, 문자가 들어왔으면 그 포켓몬의 이름에 해당하는 번호를 출력하면 돼. 그럼 땡큐~
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>HashMap 미사용시 시간초과</li>
<li>'<index, 문자열>', '<문자열, index>' 두 종류 필요</li>
<li>두 종류의 맵을 모두 문자열로 입력받아 하나의 맵에서 검색 가능하게 만듦</li>
</ul>


<h3>풀이1(시간초과)</h3>
<pre>
<ul>
<li>ArrayList를 통해 입력받은 값이 존재하면 인덱스 위치 출력, 없으면 숫자로 인식하고 인덱스 값 출력</li>
<li>'입력으로 들어오는 문자는 반드시 도감에 있는 포켓몬의 이름만 주어져' 이라는 조건 하에 가능</li>
<li>출력에는 문제 없으나 시간초과 발생</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.List;

public class Main{
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);
        List<String> dict = new ArrayList<>();

        for(int i = 0; i < N; i++){
            dict.add(br.readLine());
        }
        for(int j = 0; j < M; j++){
            String search = br.readLine();
            int index = dict.indexOf(search);
            if(index == -1){
                bw.write(dict.get(Integer.parseInt(search)-1)+"\n");
            }else{
                bw.write(index+1+"\n");
            }
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
<li>위와 같은 방식으로 풀이</li>
<li>BufferedWriter 보다 StringBuilder 속도가 더 빠름</li>
<li><a href='https://chb2005.tistory.com/73'>참고</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.List;

public class Main{
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);
        List<String> dict = new ArrayList<>();

        for(int i = 0; i < N; i++){
            dict.add(br.readLine());
        }
        for(int j = 0; j < M; j++){
            String search = br.readLine();
            int index = dict.indexOf(search);
            if(index == -1){
                sb.append(dict.get(Integer.parseInt(search)-1)).append("\n");
            }else{
                sb.append(index + 1).append("\n");
            }
        }
        System.out.print(sb);
    }
}

</code>
</pre>

</code>
</pre>

<h3>풀이3(정답)</h3>
<pre>
<ul>
<li>HashMap 사용하여 조회 속도 상승</li>
<li>두 종류를 하나로 입력받아 이름이나 번호 둘다 조회 가능</li>
</ul>
<code>
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

public class Main{
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        String NM = br.readLine();
        int N = Integer.parseInt(NM.split(" ")[0]);
        int M = Integer.parseInt(NM.split(" ")[1]);
        Map<String, String> dictMap = new HashMap<>();

        for(int i = 0; i < N; i++){
            String name = br.readLine();
            String index = Integer.toString(i + 1);
            dictMap.put(name, index);
            dictMap.put(index, name);
        }
        for(int j = 0; j < M; j++){
            sb.append(dictMap.get(br.readLine())).append('\n');
        }
        System.out.print(sb);
    }
}

</code>
</pre>
