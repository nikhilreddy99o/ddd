CREATE FUNCTION ami_workspace.test.double_up_test(x integer)
  RETURNS integer
  LANGUAGE PYTHON
  WITH (handler = 'twice')
  AS $$
  def twice(a):
      return a * 2
  $$;
