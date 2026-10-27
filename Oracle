# 특정 월 데이터 조회 및 월별 집계

## 1. 학습 목표

Oracle SQL에서 날짜 함수를 활용하여 특정 월의 데이터를 조회하고, 월별 수량을 집계하는 방법을 학습한다.

**핵심 개념**

- `TO_CHAR()` : 날짜를 원하는 문자열 형식으로 변환
- `TO_DATE()` : 문자열을 날짜 타입으로 변환
- `ADD_MONTHS()` : 날짜에 개월 수 더하기
- `SUM()` : 수치 합계 계산
- `GROUP BY` : 동일한 기준으로 데이터 그룹화

---

## 2. 최종 SQL 쿼리

```sql
SELECT
    TO_CHAR(T.CREATED_AT, 'YYYY-MM') AS TARGET_MONTH,
    SUM(T.QUANTITY) AS TOTAL_QTY
FROM SAMPLE_TABLE T
WHERE T.CATEGORY_ID = 'A001'
  AND T.CREATED_AT >= TO_DATE('2026-09', 'YYYY-MM')
  AND T.CREATED_AT < ADD_MONTHS(
      TO_DATE('2026-09', 'YYYY-MM'), 1
  )
GROUP BY TO_CHAR(T.CREATED_AT, 'YYYY-MM');
```

### 쿼리 설명

| 구문 | 역할 |
|---|---|
| `TO_CHAR(CREATED_AT, 'YYYY-MM')` | 날짜를 연-월 문자열로 변환 |
| `SUM(QUANTITY)` | 수량 합계 계산 |
| `CATEGORY_ID = 'A001'` | 특정 분류 데이터만 조회 |
| `>= TO_DATE(...)` | 해당 월의 시작일부터 조회 |
| `< ADD_MONTHS(...)` | 다음 달 시작일 이전까지만 조회 |
| `GROUP BY` | 월별 데이터 그룹화 |

---

## 3. 가장 중요한 패턴

```sql
-- 특정 월의 데이터 조회
WHERE T.CREATED_AT >= TO_DATE('2026-09', 'YYYY-MM')
  AND T.CREATED_AT < ADD_MONTHS(
      TO_DATE('2026-09', 'YYYY-MM'), 1
  )
```

이 조건은 다음 범위를 의미한다.

```text
2026-09-01 00:00:00 이상
        ↓
2026-10-01 00:00:00 미만
```

즉, **2026년 9월에 해당하는 데이터만 조회**한다.

---

## 4. 한 줄 정리

> Oracle에서 월 단위 조회 시 `TO_DATE()`와 `ADD_MONTHS()`로 날짜 범위를 지정하고, `TO_CHAR()`와 `GROUP BY`를 사용해 데이터를 집계한다. 날짜 컬럼에 함수를 직접 적용하지 않는 범위 조건이 일반적인 인덱스 활용에 유리하다.
