CREATE FUNCTION default.double_up(x integer)
  RETURNS integer
  LANGUAGE PYTHON
  WITH (handler = 'twice')
  AS $$
  def twice(a):
      return a * 2
  $$;
