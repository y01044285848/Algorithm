# 24060 알고리즘 수업 - 병합 정렬 1

<h3>요약</h3>
<ul>
  <li>주어진 코드를 적용</li>
  <li>재귀를 사용하나 영향이 적음</li>
</ul>


<h3>풀이(정답)</h3>
<ul>
  <li>정렬 문제로 병합 정렬에 대한 내용</li>
  <li>문제에서 병합 정렬의 의사코드가 주어짐</li>
  <li>Java로 적용시킴</li>
</ul>
<pre>
<code>

import java.io.*;
import java.util.StringTokenizer;

public class Main {

    static int[] tmp;
    static int result = -1;
    static int cnt = 0;
    static int K;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        int[] A = new int[N];
        tmp = new int[N];

        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(st.nextToken());
        }

        merge_sort(A, 0, N - 1);

        System.out.println(result);
    }

    static void merge_sort(int A[], int p, int r) {
        if (p < r) {
            int q = (p + r) / 2;
            merge_sort(A, p, q);
            merge_sort(A, q + 1, r);
            merge(A, p, q, r);
        }
    }

    static void merge(int A[], int p, int q, int r) {
        int i = p;
        int j = q + 1;
        int t = 0;

        while (i <= q && j <= r) {
            if (A[i] < A[j]) {
                tmp[t++] = A[i++];
            } else {
                tmp[t++] = A[j++];
            }
        }

        while (i <= q) {
            tmp[t++] = A[i++];
        }

        while (j <= r) {
            tmp[t++] = A[j++];
        }

        i = p;
        t = 0;
        while (i <= r) {
            cnt++;

            if (cnt == K) {
                result = tmp[t];
                break;
            }

            A[i++] = tmp[t++];
        }
    }
}

</code>
</pre>
