# 1764 스택(https://www.acmicpc.net/problem/10828)

<h3>문제</h3>
<ul>
  <li>정수를 저장하는 스택을 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오.

명령은 총 다섯 가지이다.

- push X: 정수 X를 스택에 넣는 연산이다.
- pop: 스택에서 가장 위에 있는 정수를 빼고, 그 수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.
- size: 스택에 들어있는 정수의 개수를 출력한다.
- empty: 스택이 비어있으면 1, 아니면 0을 출력한다.
- top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.</li>
<li>입력
  <pre>
첫째 줄에 주어지는 명령의 수 N (1 ≤ N ≤ 10,000)이 주어진다. 둘째 줄부터 N개의 줄에는 명령이 하나씩 주어진다. 주어지는 정수는 1보다 크거나 같고, 100,000보다 작거나 같다. 문제에 나와있지 않은 명령이 주어지는 경우는 없다.
  </pre>
  </li>
<li>출력
  <pre>
  출력해야하는 명령이 주어질 때마다, 한 줄에 하나씩 출력한다.
  </pre>
  </li>
</ul>

<h3>요약</h3>
<ul>
<li>Bufferedwriter 사용 안하면 시간초과!</li>
<li>스택의 기본 구조를 묻는 문제</li>
</ul>


<h3>풀이(정답)</h3>
<ul>
  <li>push는 뒤에 숫자도 입력받아 혼자 형식이 다름 -> default로 처리</li>
  <li>default로 처리하여 split횟수 줄이려했는데 의미 없는거 같음</li>
</ul>
<pre>
<code>
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.Stack;

public class Main{
    public static void main(String[] args) throws IOException{
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int commends = Integer.parseInt(br.readLine());

        Stack<Integer> stackInt = new Stack<>();

        for (int i = 0; i < commends; i++) {
            String commendString = br.readLine();
            switch (commendString) {
                case "empty":
                    if(stackInt.empty()){
                        bw.write("1\n");
                    }else{
                        bw.write("0\n");
                    }
                    
                    break;
                case "size":
                    bw.write(stackInt.size()+"\n");
                    break;
                case "top":
                    
                    if(stackInt.empty()){
                        bw.write("-1\n");
                    }else{
                        bw.write(stackInt.peek()+"\n");
                    }
                    break;

                case "pop":

                    if(stackInt.empty()){
                        bw.write("-1\n");
                    }else{
                        bw.write(stackInt.pop()+"\n");
                    }
                    break;

                default:
                    stackInt.push(Integer.parseInt(commendString.split(" ")[1]));
                    break;
            }
        }
        bw.flush();
        bw.close();
    }
}

</code>
</pre>