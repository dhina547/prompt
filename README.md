SELECT *
FROM (
    SELECT t.*,
           ROW_NUMBER() OVER (
               PARTITION BY BUSINESS_DATE
               ORDER BY ROWID
           ) AS rn
    FROM LEDGER_MASTER_MONTHLY_HIST t
    WHERE BUSINESS_DATE IN (
        DATE '2025-12-31',
        DATE '2025-10-31',
        DATE '2025-06-30',
        DATE '2025-11-30',
        DATE '2026-06-30',
        DATE '2025-08-31',
        DATE '2025-07-31',
        DATE '2026-07-31',
        DATE '2026-03-31',
        DATE '2026-05-31',
        DATE '2026-04-30',
        DATE '2026-01-31',
        DATE '2026-02-28'
    )
)
WHERE rn <= 3847
FETCH FIRST 50000 ROWS ONLY;
