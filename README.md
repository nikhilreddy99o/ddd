WITH FUNCTION double_up(x integer) 
    RETURNS integer 
    LANGUAGE PYTHON 
    WITH (handler = 'twice') 
    AS $$ 
    def twice(a): 
        return a * 2 
    $$

SELECT double_up(5);  -- Output: 10
