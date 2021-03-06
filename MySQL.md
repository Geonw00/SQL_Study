# SQL_Study(MySQL)

SELECT
-------------
- 기본형식: 
```    
    - SELECT 열 이름 FROM 테이블 이름 [WHERE 조건]
```

- 전체 컬럼 조회:
```
    - SELECT * FROM 테이블 이름
```

- 컬럼명 변경하여 조회
```
    - SELECT 열 이름 AS 변경할 이름 FROM 테이블 이름
```

- 정렬(오름차순):
```
    - SELECT 열 이름 FROM 테이블 이름 ORDER BY 정렬기준 열 이름 ASC   
    - SELECT 열 이름 FROM 테이블 이름 ORDER BY 정렬기준 열 이름
```

- 정렬(내림차순):
```
    - SELECT 열 이름 FROM 테이블 이름 ORDER BY 정렬기준 열 이름 DESC
```

- 특정 열의 특정 값을 가진 데이터만 조회
```
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 = 특정 값
```

- 특정 열의 특정 값을 가지지 않은 데이터만 조회
```
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 != 특정 값
```

- 출력데이터 행 개수 제한
```
    - SELECT 열 이름 FROM 테이블 이름 LIMIT 제한할 수 
    
    EX) 5개의 데이터를 출력하고 싶은 경우
    - SELECT 열 이름 FROM 테이블 이름 LIMIT 5
    
    EX) 5번째 데이터 부터 3개의 데이터를 출력해야하는 경우(INDEX는 0부터 시작)
    - SELECT 열 이름 FROM 테이블 이름 LIMIT 4, 3
```

- 최댓값
```
    - SELECT MAX(열 이름) FROM 테이블 이름   
```

- 최솟값
```
    - SELECT MIN(열 이름) FROM 테이블 이름
```

- 해당 열의 데이터 수 (COUNT)
```
    - SELECT COUNT(열 이름) FROM 테이블 이름 
```

- 해당 열의 중복되지 않는 데이터 수 
```
    - SELECT COUNT(DISTINCT(열 이름)) FROM 테이블 이름 
```

- 특정 열의 데이터가 NULL인 데이터 조회
```
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 IS NULL
```

- 특정 열의 데이터가 NULL이 아닌 데이터 조회
```
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 IS NOT NULL
```

- 특정 열의 데이터가 NULL인 경우 값 변경 후 데이터 조회
```
    - SELECT IFNULL(열 이름, 변경할 값) FROM 테이블 이름
```

- 특정 열을 기준으로 같은 값을 가지는 데이터끼리 그룹화하여 조회 (GROUP BY)
```
    - SELECT 열 이름 FROM 테이블 이름 GROUP BY 그룹화할 기준 열
```

- 그룹화 이후 특정 기준에 부합하는 데이터 조회 (HAVING)
```
    - SELECT 열 이름 FROM 테이블 이름 GROUP BY 그룹화할 기준 열 HAVING 조건
    
    EX) 그룹의 수가 1보다 큰 그룹의 데이터만 조회
    - SELECT 열 이름 FROM 테이블 이름 GROUP BY 그룹화할 기준 열 HAVING COUNT(그룹화할 기준 열) > 1
```


- 날짜 데이터 사용
```
    YEAR : 년
    MONTH : 월
    DAY : 일
    HOUR : 시
    MINUTE : 분
    SECOND : 초
    DATE_FORMAT : 날짜형식 조절 가능
    
    EX) 기준 날짜형식에서 월만 시간만 추출하여 출력할 경우
    - SELECT HOUR(열 이름) FROM 테이블 이름
    
    EX) YYYY-MM-DD만 출력하고 싶을 경우
    - SELECT DATE_FORMAT(열 이름, '%Y-%m-%d') FROM 테이블 이름
```

- 가상의 테이블 생성
```
    - WITH RECURSIVE 생성할 테이블 명 AS (
      SELECT 시작 값 AS 생성할 컬럼 명
      UNION ALL
      SELECT 시작값부터 생성할 조건 FROM 생성할 테이블 명 WHERE 종료 조건)
    
    EX) 0 ~ 23의 데이터 값을 가지는 HOUR열을 가지는 REC 테이블 생성  
    - WITH RECURSIVE REC AS (
      SELECT 0 AS HOUR
      UNION ALL
      SELECT HOUR+1 FROM REC WHERE HOUR < 23)
```

- LIKE문 사용
```
    _ : 한 문자 의미
    % : 모든 문자 의미
    
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 LIKE 조건
    
    EX) 두 번째 단어부터 MOUSE가 포함되는 데이터 조회할 경우
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 LIKE '_MOUSE'
    
    EX) 단어위치 상관없이 MOUSE가 포함되는 데이터 조회할 경우
    - SELECT 열 이름 FROM 테이블 이름 WHERE 특정 열 이름 LIKE '%MOUSE%'
```

JOIN
-------------
- LEFT JOIN (좌측 테이블을 기준으로 JOIN 실행 => 우측 테이블 값이 NULL일 경우 NULL 상태로 붙음)
```
    - SELECT 열 이름 FROM 좌측 테이블명 LEFT JOIN 우측 테이블명 ON 테이블 간의 연결조건
```

- RIGHT JOIN (우측 테이블을 기준으로 JOIN 실행 => 좌측 테이블 값이 NULL일 경우 NULL 상태로 붙음)
```
    - SELECT 열 이름 FROM 좌측 테이블명 RIGHT JOIN 우측 테이블명 ON 테이블 간의 연결조건
```

- INNER JOIN (양 테이블 모두 데이터가 존재할 경우만 JOIN)
```
    - SELECT 열 이름 FROM 좌측 테이블명 JOIN 우측 테이블명 ON 테이블 간의 연결조건
    - SELECT 열 이름 FROM 좌측 테이블명 INNER JOIN 우측 테이블명 ON 테이블 간의 연결조건
    - SELECT 열 이름 FROM 좌측 테이블명 JOIN 우측 테이블명 WHERE 테이블 간의 연결조건
```

- JOIN시 특정 테이블의 특정 열 조회
```
    - SELECT 테이블 명.열 이름 FROM 좌측 테이블명 JOIN 우측 테이블명 ON 테이블 간의 연결조건
    
    AS를 통해 테이블명을 쉽게 재지정하여 사용하면 편함
```

- 셀프 JOIN
```
    EX) INNER JOIN으로 셀프조인을 진행할 경우
    - SELECT 열 이름 FROM 테이블명 테이블 별칭1 JOIN 테이블명 테이블 별칭2 ON 테이블 간의 연결조건
    
    EX) LEFT JOIN으로 셀프조인을 진행할 경우(RIGHT도 방식은 동일)
    - SELECT 열 이름 FROM 테이블명 테이블 별칭1 LEFT JOIN 테이블명 테이블 별칭2 ON 테이블 간의 연결조건
```
