

**Activity 1: Simple Selection**

* Description: List all vehicles with type 'Compact SUV' and price below 30,000.00.

script:

```sql

SELECT
	nome AS name,
	tipo AS type,
	valor AS value
FROM
	public.veiculos v
WHERE
	tipo LIKE 'SUV Compacta'
	AND valor < 30000.00;


```

**Activity 2: Simple Join**

* Description: Display the names of customers and the names of the dealerships where they made their purchases.

script:
```sql
SELECT
	cliente as client,
	con.concessionaria as dealership
FROM
	public.clientes c
JOIN concessionarias con ON
	c.id_concessionarias = con.id_concessionarias;


```

**Activity 3: Counting and Grouping**

* Description: Count the number of salespeople at each dealership.

script:
```sql
SELECT
	COUNT(id_vendedores) AS number_sellers,
	c.concessionaria AS dealership
FROM
	vendedores v
JOIN concessionarias c ON
	v.id_concessionarias = c.id_concessionarias
GROUP BY
	c.concessionaria;

```


**Activity 4: Subquery**

* Description: Find the most expensive vehicles sold in each vehicle type.

script:

```sql
SELECT
	tipo AS type,
	MAX(valor_pago) AS max_value
FROM
	vendas
JOIN veiculos v ON vendas.id_veiculos = v.id_veiculos 
GROUP BY
	v.tipo;

```


**Activity 5: Multiple Join**

* Description: List the customer's name, the purchased vehicle, and the amount paid for all sales.

script:

```sql
SELECT
	cl.cliente AS client,
	v.nome AS vehicle,
	vd.valor_pago AS pay_value
FROM
	vendas vd
JOIN clientes cl ON
	vd.id_clientes = cl.id_clientes
JOIN veiculos v ON
	vd.id_veiculos = v.id_veiculos;


```


**Activity 6: Filter with Aggregation**

* Description: Identify the dealerships that sold more than 5 vehicles.

script:

```sql
SELECT 
	COUNT(id_vendas) AS num_sells,
	c.concessionaria AS dealers
FROM 
	vendas v 
JOIN 
	concessionarias c ON v.id_concessionarias = c.id_concessionarias 
GROUP BY 
	c.concessionaria
HAVING 
	COUNT(id_vendas) > 5;
```


**Activity 7: Query with ORDER BY and LIMIT**

* Description: List the three most expensive vehicles available.

script:

```sql
SELECT
	nome AS name,
	valor AS value
FROM
	veiculos v
ORDER BY
	valor DESC
LIMIT 3;

```
**Activity 8: Query with Dates**

* Description: Select all vehicles added in the last month.
  
script:


```sql

SELECT
	nome AS name,
	data_inclusao AS inclusion_data
FROM
	veiculos
WHERE
	data_inclusao > CURRENT_TIMESTAMP - INTERVAL '1 month';


```


**Activity 9: Outer Join**

* Description: List all cities and any dealerships in them, if any.
  
script:

```sql
SELECT
	cidade AS city,
	co.concessionaria AS dealership
FROM
	cidades c
JOIN concessionarias co ON
	c.id_cidades = co.id_cidades;

```

**Activity 10: Query with Multiple Conditions**

* Description: Find customers who bought 'Premium Hybrid SUV' vehicles or vehicles priced above 60,000.00.

script:

```sql
SELECT 
	c.cliente AS client,
	vei.tipo AS vehicle_type,
	valor_pago AS pay_value
FROM 
	vendas v 
JOIN 
	clientes c ON v.id_clientes = c.id_clientes 
JOIN 
	veiculos vei ON v.id_veiculos = vei.id_veiculos 
WHERE 
	vei.tipo LIKE 'SUV Premium Híbrida' OR valor_pago > 60000.00;
```
