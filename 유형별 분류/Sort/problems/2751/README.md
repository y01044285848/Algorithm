# 2571 수 정렬하기2

<h3>요약</h3>
<ul>
  <li>1차원 리스트 정렬 문제</li>
  <li>일반적인 정렬 방식을 택할 경우 시간 초과(극단적 예시 포함)</li>
  <li>시간 편차가 적은 알고리즘 필요</li>
</ul>

<h3>참고</h3>
<pre>
일반적으로 Array.sort()를 이용한 정렬을 많이 사용하나 시간초과 발생</br>
이외에 Collections.sort()도 많이 사용
    <table>
      <tr>
        <td></td>
        <th>정렬 방식</td>
        <th>시간 복잡도</td>
      </tr>
      <tr>
        <th>Arrays.sort()</th>
        <td>DualPivotQuicksort</td>
        <td>평균 : O(nlog(n)) / 최악 : O(n^2)</td>
      </tr>
      <tr>
        <th>Collections.sort()</th>
        <td>TimeSort (삽입정렬과 합병정렬을 결합한 정렬)</td>
        <td>평균, 최악 : O(nlog(n))</td>
      </tr>
    </table>
퀵정렬 최악의 경우 O(n^2)이 넘어가 시간초과를 유발
</pre>


<h3>풀이</h3>
<pre>
<code>
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
public class J2751 {

	public static void main(String[] args) throws NumberFormatException, IOException {
		
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int N = Integer.parseInt(br.readLine()); 

        ArrayList<Integer> list = new ArrayList<>();

        for(int i = 0; i < N; i++){
            list.add(Integer.parseInt(br.readLine()));
        }

        Collections.sort(list);

        for(int num : list){
            bw.write(num+"\n");
        }

        bw.flush();
        bw.close();
      }
    }
</code>
</pre>
