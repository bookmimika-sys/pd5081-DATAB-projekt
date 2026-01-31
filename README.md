## Wyniki zapyta SQL

### Zapytanie 2: Testy z więcej niż z 30 pacjentami
```sql
select test_type,
count(distinct patient_id)
from patient_test
left join tests on tests.test_id = patient_test.test_id
group by test_type
having count(distinct patient_id) > 30;
```
**Wynik:**

| test_type | count(distinct patient_id) |
|-----------|----------------------------|
| NGS-panel |                         38 |
| SNP Array |                         39 |


### Zapytanie 2: Nazwy testów i obliczoną średnią liczbę wariantów dla każdego testu
```sql
select test_type,
avg(var_count)
from tests
left join (select test_id,
count(distinct variant) as var_count
from results group by test_id) vars on vars.test_id = tests.test_id
group by test_type;
```
**Wynik:**
| test_type | avg(var_count) |
|-----------|----------------|
| SNP Array |         2.3400 |
| NGS-panel |         2.7143 |
| WES       |         2.7059 |
| WGS       |         2.6429 |


