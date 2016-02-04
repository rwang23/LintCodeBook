###OverLoading

	public int distance(double a, double b)
	public double distance(double a, double b)
	是不合法的,不能这样overload
	除非parameter list也是不同的

###Public vs Private
####For variable
	private means only accessable within class
	so that we can use getter and setter, giving us more control
####For functions
