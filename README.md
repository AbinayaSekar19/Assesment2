using System;
using System.Data;
using System.Data.SqlClient;


class Program
{
    static void Main(string[] args)
    {
        string connectionString = "Data Source=(localdb)\\mssqllocaldb;Initial Catalog = model;Integrated Security=True;";
        using (SqlConnection connection = new SqlConnection(connectionString)) 
        {
            try
            {
                connection.Open();

                GetOrdersWithCustomers(connection);

           
            }
            catch (Exception ex) 
                { 
                    Console.WriteLine("Error: " + ex.Message);
                } 
        }
    }
    static void GetOrdersWithCustomers(SqlConnection connection)
    {
        string query = "GetOrdersWithCustomers";
        using (SqlCommand command = new SqlCommand(query, connection))
        {
            command.CommandType = System.Data.CommandType.StoredProcedure;
            using (SqlDataReader reader = command.ExecuteReader())
            {
                while(reader.Read())
                {
                    Console.WriteLine($"OrderId:{reader["OrderId"]}, CustomerId:{reader["CustomerId"]},CompanyName:" +
                        $"{reader["CompanyName"]},OrderDate:{reader["OrderDate"]},ShippedDate:{reader["ShippedDate"]}");
                }
            }        
        }
    }
}
