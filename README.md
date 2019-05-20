# Perl-Scripting

This Perl scripting program was completed as a part of a online programming course which introduced me into the basics of Perl.
The projects involved opening an external file. Reading from this file. Writing to this file. Displaying the contents of the file.
Various Perl entities were used to complete this project which included subroutines, arrays, loops, conditional branchs.

----

## Requirements

Design a Perl script which reads from a file 'Customers.txt'. The program must provide four options. First, Search for a customer.
Second, add a new customer. Third, display all the customers. Fourth, to exit back to code. While designing the script consider all
corner cases. Example: the case where when incorrect option is selected.

----
## Code

```PERL
###### This project must be designed to do 4 funtions.	##############
######	Initially, have a list of customers stored as 'Customer.txt' #
######	We must first be able to search for customer.		######		
######	Second, we must be able to add a new customer.		######
######	Third, we must be able to print all customers.		######
######	Final option must let us come out of the program.	######
######################################################################

# To start, let us first define the different subroutines.
# First, we have to store the customer name into an array to access and display locally
# my_names will hold all the names in the customer.txt
sub read_customer
{
	@my_names = ();
	$filename = 'Customers.txt';
	open(FILE, "<", $filename);
	
	while( chomp($name=<FILE>))
	{
		push(@my_names,$name);
	}
	close(FILE);
}

# Displays the option menu and returns the value of the selected option

sub option_menu
{
	#Print message for the user to let him know the various available options.
	print("\n\nSelect an option. \n 1. Find a customer \n 2. Add a customer \n 3. Display all customer \n 4. Quit \n");
	chomp($option = <STDIN>);
	
	# Returns the option that was selected
	return $option;
}

# Subroutine that displays all the customers in the List

sub displayall_customer
{
	print(" The customers are \n");
	my $count=0;
	foreach $val(@my_names)
	{
		$count= $count + 1;
		print(" $count. $val\n")
	}
}

# Subroutine to add a new customer to the list

sub add_customer
{
	print("\n Enter the name of the customer\n");
	chomp($new_name = <STDIN>);
	
	$status = push(@my_names,$new_name);	#Adds the new customer into the list
	
	if ($status)
	{
		print("New customer added\n");
	}
	else
	{
		print("Something went wrong. Try again\n");
	}
}

# Subroutine to search for a customer

sub search_customer
{
	print("\n Enter the name of the customer\n");
	chomp($search=<STDIN>);
	
	#To see if there exists a name similar to name
	foreach $name(@my_names)
	{
		if( lc($name)eq lc($search))
		{
			print("\n $name was found \n");
			return;
		}
	}
}

#######################################################################################
########	Now that we have defined the subroutines, now to call them	#######
#######################################################################################

&read_customer();	# Gets the list of all customers from the text file.

$option_sel = &option_menu();	# Print and retrieves the option

while ( $option != 4)
{
	if($option_sel == 1)
	{
		&search_customer();	# Executes the search subroutine
		$option_sel = &option_menu();	# Gives the user option menu again
	}
	elsif($option_sel == 2)
	{
		&add_customer();	# Executes the add customer subroutine
		$option_sel = &option_menu();	# Gives the user option menu again
	}
	elsif($option_sel == 3)
	{
		&displayall_customer();	# Executes the display subroutine
		$option_sel = &option_menu();	# Gives the user option menu again
	}
	else
	{
		print("Enetr a valid option\n");
		$option_sel = &option_menu();
	}
}

# Once the customers are added, we need to save them on the text file as well. Now we shall do that
$filename='Customers.txt';
open(FILE, ">>", $filename);
foreach $nameF(@my_names)
{
	chomp($name);
	print(FILE "$nameF\n");
}
close(FILE);

exit;

```

