CREATE  DEFINER = 'root'@'localhost' PROCEDURE account_count()
SQL SECURITY INVOKER
BEGIN
SELECT 'Number of accounts:', COUNT(*) FROM mysql.user;
END


call account_count()