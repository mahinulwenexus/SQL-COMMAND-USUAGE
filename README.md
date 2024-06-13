If the columns of both tables are the same, you can use a UNION
```sql
SELECT X.*
  FROM ( SELECT `id`,
                `userID`,
                 'INVOICE' AS PTYPE
                 `amount`,
                 `date`
            FROM `invoices`
           WHERE {$userID} = userID  
          UNION
          SELECT `id`,
                 `userID`,
                 'PAYMENT' AS PTYPE
                 `amount`,
                 `date`
            FROM `payments`
           WHERE {$userID} = userID  
        ) X
 ORDER BY X.`date`

```

EDIT

Read the relevant section of the MySQL manual on UNIONS. There are other ways of phrasing this, but this is my preferred style - it should be clear to anybody reading that the ORDER BY clause applies to the result of both sides of the UNION. A carelessly written UNION - even with an ORDER BY - may still leave the final resultset in indeterminate order.

The purpose of the PTYPE is that this query returns an extra column called PTYPE, that indicates whether each individual row is an INVOICE or a PAYMENT... ie. which of the two tables it comes from. It's not mandatory, but can often be useful within a union

# SQL-COMMAND-useages
