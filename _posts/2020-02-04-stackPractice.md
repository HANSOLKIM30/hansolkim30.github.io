---
title: "[ALGORITHM] 자료구조 1 - 연습문제"
categories: ALGORITHM
date: 2020-02-04
---


# [자료구조 1 - 연습문제]
스택을 이용하는 문제들을 풀어보자.<br>
1. 단어뒤집기 2
2. 쇠막대기 
3. 오큰수
4. 오등큰수

## 단어뒤집기 2
- [단어뒤집기 2](https://www.acmicpc.net/problem/17413)<br>
```java    
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        
        Stack<Character> stack = new Stack<Character>();
        
        String str = br.readLine();
        str += '\n';	//마지막엔 공백이 오지 못하므로, 마지막 단어가 tag 단어 아닐 경우 뒤집어주기 위해 넣어준다.
        
        boolean tag = false;	//tag의 내부에 있는지를 나타내는 변수
        
        for(char ch : str.toCharArray()){	//String을 toCharArray 메서드를 통해 char 타입의 배열로 변경
            if(ch == '<'){	//'<'만났을 경우
                while(!stack.isEmpty()){
                    bw.write(stack.pop());	//일반단어와 tag가 공백으로 구분되어있지 않는 경우가 있으므로 <만났을 경우 일반단어 모두 뒤집어 출력
                }
                tag = true; 
                bw.write(ch);
            } else if(ch=='>'){    //'>'만났을 경우
                bw.write(ch);
                tag = false;
            } else if(tag == true){    //tag가 true인 경우
                bw.write(ch);
            } else{    //<> 안에 있는 문자가 아닐 경우
                if(ch == ' ' || ch == '\n'){    //공백 만났을 경우
                    while(!stack.isEmpty()){
                    bw.write(stack.pop());	//뒤집어서 출력
                }
                    bw.write(ch);//공백 출력
                } else{
                    stack.push(ch);    //공백이 아닐 시 stack에 push
                }
            }
        }
        bw.flush();
        bw.close();
    }
```

##  쇠막대기
- [쇠막대기](https://www.acmicpc.net/problem/10799)<br>
```java
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        char[] charArray = str.toCharArray();
        
        int num = 0;	//레이저에 잘린 조각
        
        Stack<Integer> stack = new Stack<Integer>();
        
        for(int i = 0; i < charArray.length; i++){
            if(charArray[i]=='('){
                stack.push(i);
            } else{	//')'를 만났을 때
                if(stack.peek()+1 ==i){	//stack에 저장된 맨 위의 인덱스와 1차이가 난다면 레이저 의미	
                   stack.pop();	//다음 인덱스로 넘어가기 위해 pop
                   num += stack.size();	//pop한 뒤 stack안에 남은 (만큼 레이저가 적용되는 쇠막대기가 있으므로 size를 더해준다.
                } else{	//차이가 1보다 크다면 쇠막대기 의미(쇠막대기의 끝) 
                  stack.pop();
                  num += 1;	//하나의 막대기를 하나의 레이저로 자를 경우 2조각임을 기억하자. 쇠막대기가 끝났으므로 레이저로 자르고 남은 쇠막대기 +1을 해준다.
                }                
            }
        }
        
        System.out.println(num);
    }
```

## 오큰수
- [오큰수](https://www.acmicpc.net/problem/17298)<br>
```java
    public static void main(String[] args) throws IOException{
        Stack<Integer> stack = new Stack<Integer>();
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = Integer.parseInt(br.readLine());    //수열 a의 크기 num
        int[] a = new int[n];    //입력받은 수열 a
        int[] nge = new int[n];    //오큰수의 배열

        String[] strArray = br.readLine().split(" ");    //공백 단위로 나눠서 String 배열에 저장
        
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(strArray[i]);    //정수형으로 변형
        }
        
        stack.push(0);    //0번 인덱스는 무조건 들어가야하므로 push
        
        for(int i = 1; i < n; i++){
           while(!stack.isEmpty() && a[stack.peek()] < a[i]) //stack이 비어있으면 peek처리 못하고 런타임에러나므로 isEmpty로 꼭 확인{
			/*예) stack 안의 숫자가 543이고 a[i]가 6일 경우 스택 안의 수들의 오큰수는 모두 6이기 때문에 while문으로 계속해서 pop하면서 neg 배열에 저장*/
                   nge[stack.pop()] = a[i];
           }
           stack.push(i);      
        }
        
         while (!stack.empty()) {    //for문 한바퀴 다 돌고 나온 경우, 더이상 오큰수가 없으므로 -1처리
            nge[stack.pop()] = -1;
        }
        
        for(int i = 0; i < n; i++){
            bw.write(nge[i] + " ");
        }
        bw.write("\n");
        bw.flush();
        bw.close();
    }
```

## 오등큰수
- [오등큰수](https://www.acmicpc.net/problem/17299)<br>
```java
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        Stack<Integer> stack = new Stack<Integer>();
        
        int n = Integer.parseInt(br.readLine());
        int[] a = new int[n];
        int[] cnt = new int[1000001];	//가능한 최대 수열의 크기 
        int[] ngf = new int[n];
        
        String str = br.readLine();
        String[] strArray = str.split(" ");
        for(int i = 0; i < n; i++){
            a[i] = Integer.parseInt(strArray[i]);
            cnt[a[i]] += 1;	
            /*이중 for문으로 체크하면 시간복잡도 상승하므로
            cnt[a[i]]로 처리해서 배열이 지니는 각각의 숫자를 센다.*/
        }
        
        stack.push(0);
        
        for(int i = 1; i < n; i++){
            while(!stack.isEmpty() && cnt[a[stack.peek()]] < cnt[a[i]]){
                ngf[stack.pop()] = a[i];
            }
            stack.push(i);
        }
        
        while(!stack.isEmpty()){
            ngf[stack.pop()] = -1;
        }
        
        for(int i = 0; i < n; i++){
            bw.write(ngf[i] + " ");
        }
        
        bw.write("\n");
        bw.flush();
        bw.close();
    }
```
