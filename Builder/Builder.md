# Builder
This pattern is creational pattern.
It is ment to be used in order to simplify the process of construction of complex objects. 
It can also be used to solidify the rules of configuring object.
We can find some good examples of Builder pattenr in .NET Base Class Library.

System.Data.SqlClient.SqlConnectionStringBuilder is an example of a latter type of a builder pattern. It provides a clear way to construct a connection string for a consumer.

Microsoft.AspNetCore.Hosting.WebHostBuilder is another example of a builder design pattern. It provides an interface to configuring an IWebHost object responsibe for running the web application.

`Microsoft.EntityFrameworkCore.ModelBuilder` and related `Microsoft.EntityFrameworkCore.Metadata.Builders.EntityTypeBuilder` are yet another examples of a builder pattern.  
> They provide "a simple API surface for configuring a IMutableModel that defines the shape of your entities, the relationships between them, and how they map to the database" \
>– MSDN

It is common for a builder class methods to return a builder type object. This way builder methods can be chained, and the builder is called fluent builder.

``` csharp
namespace HotDrinkBuilderExample {
	public interface IHotDrink {
		void Drink();
	}
	public interface IHotDrinkBuilder {
		IHotDrinkBuilder UseSteelMug();
		IHotDrinkBuilder UseGlassMug();
		IHotDrinkBuilder UseCeramicMug();
		IHotDrinkBuilder UseGroundCoffee();
		IHotDrinkBuilder UseInstantCoffee();
		IHotDrinkBuilder UseTea();
		IHotDrinkBuilder AddHotWater();
		IHotDrinkBuilder AddHotMilk();
		IHotDrinkBuilder AddSugar();
		IHotDrink Build();
	}
	//
	// ...
	//
	public class Program {
		public static void Main(string[] args) {
            IHotDrinkBuilder builder = new DefaultHotDrinkBuilder();
			IHotDrink coffee = builder.UseCeramicMug()
				.UseGroundCoffee()
				.AddHotWater()
				.AddSugar()
				.AddSugar()
				.AddSugar()
				.Build();
			coffee.Drink();
	}
}
```

