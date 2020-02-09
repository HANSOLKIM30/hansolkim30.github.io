---
title: "[ALGORITHM] 수학 1 - 연습문제"
categories: ALGORITHM
date: 2020-02-09
---


# [수학 1 - 연습문제]
[수학 1]에서 배운 이론들을 활용하는 문제들을 풀어보자.<br>
- 최대공약수
	1. GCD 합
	2. 숨바꼭질 6
- 진법 변환
	3. 2진수 → 8진수
	4. 8진수 → 2진수
	5. -2진수
- 소수
	6. 골드바흐 파티션


## GCD 합
- [GCD 합](https://www.acmicpc.net/problem/9613)
```java 
   static int gcd(int a, int b){    //유클리드 호제법
        if(b == 0){
            return a;
        } else{
            return gcd(b, a%b);
        }
    }  
    static long sumGCD(int[] a){    //합 구하기
        long sum = 0;
        for(int i = 0; i < a.length-1; i++){
            for(int j = i+1; j < a.length; j++){ 
                sum += gcd(a[i],a[j]);
            }
        }
        return sum;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);        
        int t = sc.nextInt(); //테스트 케이스의 개수
        
        while(t-- > 0){
            int n = sc.nextInt();    //수의 개수
            int[] arrN = new int[n];    //수를 저장할 배열
            for(int i = 0; i < n; i++){
                arrN[i] = sc.nextInt();    //입력으로 주어지는 수는 1000000을 넘지 않는다.
            }
            System.out.println(sumGCD(arrN));
        }
    }       
```

##  숨바꼭질 6
- [숨바꼭질 6](https://www.acmicpc.net/problem/17087)
```java
    static int gcd(int a, int b){    //유클리드 호제법
        if(b == 0){
            return a;
        } else{
            return gcd(b, a%b);
        }
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);        
        int n = sc.nextInt();    //동생의 수
        int s = sc.nextInt();    //수빈이의 위치
        int[] arr = new int[n];    //수빈이와 동생과의 거리 저장 배열
        for(int i = 0; i<n; i++){
            int a = sc.nextInt();    //수빈이 동생의 위치
            arr[i] = Math.abs(s-a);   //절대값으로 거리 저장           
        }
        int d = arr[0];    //수빈이가 이동해야 할 거리
        for(int i = 1; i < n; i++){
            d = gcd(d, arr[i]);	//배열 순서대로 비교
        }
        System.out.println(d);
    }
```

## 2진수 → 8진수
- [2진수 → 8진수](https://www.acmicpc.net/problem/1373)
```java    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        char[] ch = sc.nextLine().toCharArray();
        Queue<Character> binary = new LinkedList<Character>();
        
        if(ch.length % 3 == 2){    //3개씩 끊었을 때 앞자리 빈만큼 0채우기
            for(int i = 0; i < 1; i++){
                binary.offer('0');
            }
        } else if(ch.length % 3 == 1){
            for(int i = 0; i < 2; i++){
                binary.offer('0');
            }
        }
        
        for(int i = 0; i < ch.length; i++){    //Queue에 차례대로 넣기
            binary.offer(ch[i]);
        }
     
        while(!binary.isEmpty()){
            for(int i = 0; i < binary.size()/3 ; i++){
                System.out.print(((binary.poll()-'0')*4) + ((binary.poll()-'0')*2) + ((binary.poll()-'0')*1)); 
            }
        }
        System.out.println();
    }
```

## 8진수 → 2진수
- [8진수 → 2진수](https://www.acmicpc.net/problem/1212)<br>
```java
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();
        boolean print = false;
        int[] temp = new int[3];
        //스택을 사용하면 편리하겠지만.. 자리수가 333334나 되므로 그냥 배열만들어서 쓰자. 스택 사용하면 런타임에러 뜬다.
        
		//★ 꼭 예외처리 해주자. 이 코드 없이 0 입력하면 아무것도 안입력됨.
        if (line.length() == 1 && line.charAt(0) == '0') {
            System.out.print(0);
        }
        for(int i = 0; i < line.length(); i++){           
            int num = line.charAt(i) - '0';    //char → int 변환
            //8진수(0~7) → 2진수(0~ 111) 3자리로 표현해야하므로 최대 3번만 돌려줘도 충분.
            for(int j = 3; 0 < j; j--){     
                if(num > 0){    //num이 0이 될 때까지 2로 나누고
                    temp[j-1] = (num % 2);
                }else{    //num이 0이 되었으면 2진수 세자리 중 빈자리를 0으로 채워준다. 
                    temp[j-1] = (0);
                } 
                num/=2;    //num/2로 num 변경
            }
           
            for(int k = 0; k < 3; k++){
                if(temp[k]==1 || print==true){
                    System.out.print(temp[k]);
                    print=true;
                }
            }
        }
    }            
``` 
```java
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();
        String[] octal = {"000","001","010","011","100","101","110","111"};    //8진수는 0~7까지
        boolean print = false;
        
        if(line.length()==1 && line.charAt(0)=='0'){
            System.out.print("0");
        }
        
        for(int i = 0; i < line.length(); i++){
            int n = line.charAt(i) - '0';
            if(print == false && n < 4){    //0~3까지가 0으로 시작.
                if(n==3){
                    System.out.print("11");
                }else if(n==2){
                    System.out.print("10");
                }else if(n==1){
                    System.out.print("1");
                }else if(n==0){    //첫번째 요솟수가 0이라면 다음 요솟수도 앞에 0이 못오니까,
                    continue;    //print = false인 상태로 for문의 다음 요솟수로 이동하기 위해 for-continue처리
                }
                print = true;
            }else{
                System.out.print(octal[n]);
                print = true;    //두번째 숫자가 4이하면 바로 if절로 들어가니까 여기서도 변경
            }
        }
    }
```

## -2진수
- [-2진수](https://www.acmicpc.net/problem/2089)<br>
```java
    static void binary(int n){
        //(-2)^0 = 1, (-2)^1 = -2, (-2)^2 = 4, (-2)^3 = -8로 부호가 번갈아 나옴.
        //10진법을 -2진법으로 바꿀 때도 몫에 대한 부호를 번갈아가면서 계산.
        if(n==0){    //몫이 0이 될 때까지 binary 함수 재귀
            return;
        }
        if(n%2==0){    //2로 나누어 떨어질 때
            binary(-(n/2));
            System.out.print(0);    //나머지인 0을 출력
        } else{    //2로 나누어 떨어지지 않을 때
            if(n > 0){    //n이 양수일 때
                binary(-(n/2));
            }else{    //n이 음수일 때
                //음수를 2로 나눌 때는 몫을 주의해야 한다.
                //예)-7/2=-4...1 → (n-1)/2(음수 n에 -1을 하고 2로 나눈 것이 몫)
                //-2진수는 몫 부호를 매번 바꿔야 하므로 -(n-1)/2 = (-n+1)/2
                binary((-n+1)/2);
            }
            System.out.print(1);    //나머지인 1을 출력
        }
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        if(n == 0){    //0을 입력하면,
            System.out.println(0);    //0만 출력됨.  
        } else{
            binary(n);
        }
    }
```

## 골드바흐 파티션
- [골드바흐 파티션](https://www.acmicpc.net/problem/17103)<br>
```java
 public static void main(String[] args){
        //에라토스테네스의 체로 소수인지 여부부터 거르기
        int max = 1000000;    //주어진 최대의 수
        boolean[] prime = new boolean[max+1];    //index 1000000까지 돌리기 위해서 +1
        
        for(int i = 2; i <= max; i++){
            if(prime[i] == false){
                for(int j = i+i; j <= max; j+=i){    //i*i부터 시작해도 무방하나 나중에는 너무 커져서 런타임에러
                    prime[j] = true;
                }
            }
        }
        
        //값 입력
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();    //테스트 케이스
        
        while(t-- > 0){    //테스트 케이스만큼 실행
            int n = sc.nextInt();    //골드바흐의 추측 알아볼 숫자 입력            
            //골드바흐의 추측 실행
            int cnt = 0;    //골드바흐 추측이 몇개인지 세는 변수
            for(int i = 3; i <= n/2; i++){    //1. 홀수의 합이므로 3부터 시작 2. a+b = b+a이므로 n/2까지만 돌려보기
                if(prime[i]==false && prime[n-i]==false){
                    cnt++;
                }
            }
            System.out.println(cnt);
        }        
    }
```
