# CRUD-operations-using-Csharp-and-SQL-Server-database
#visual studio
#windows application form

-code
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace CRUDForm1
{
    public partial class Form1 : Form
    {
      
        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection("Data Source=DESKTOP-MLD0RRE\\MSSQLSERVER01;Initial Catalog=CRUDForm1;Integrated Security=True;Encrypt=False");
            con.Open();
            SqlCommand cmd = new SqlCommand("insert into student values(@ID,@Name,@Department,@Semester,@GPA)", con);
            cmd.Parameters.AddWithValue("@ID", int.Parse(textBox1.Text));
            cmd.Parameters.AddWithValue("@Name", textBox2.Text);
            cmd.Parameters.AddWithValue("@Department", textBox3.Text);
            cmd.Parameters.AddWithValue("@Semester", textBox4.Text);
            cmd.Parameters.AddWithValue("@GPA", double.Parse(textBox5.Text));
            cmd.ExecuteNonQuery();
            con.Close();

            MessageBox.Show("Successfully Inserted");

        }

        private void button2_Click(object sender, EventArgs e)
        {
         SqlConnection con = new SqlConnection("Data Source=DESKTOP-MLD0RRE\\MSSQLSERVER01;Initial Catalog=CRUDForm1;Integrated Security=True;Encrypt=False");
            con.Open();
            SqlCommand cmd = new SqlCommand("update student set Name=@Name, GPA=@GPA where ID=@ID", con);
            cmd.Parameters.AddWithValue("@ID", int.Parse(textBox1.Text));
            cmd.Parameters.AddWithValue("@Name", textBox2.Text);
            cmd.Parameters.AddWithValue("@Department", textBox3.Text);
            cmd.Parameters.AddWithValue("@Semester", textBox4.Text);
            cmd.Parameters.AddWithValue("@GPA", double.Parse(textBox5.Text));
            cmd.ExecuteNonQuery();
            con.Close();

            MessageBox.Show("Successfully Updated");
        }

        private void button3_Click(object sender, EventArgs e)
        {
            SqlConnection con = new SqlConnection("Data Source=DESKTOP-MLD0RRE\\MSSQLSERVER01;Initial Catalog=CRUDForm1;Integrated Security=True;Encrypt=False");
            con.Open();
            SqlCommand cmd = new SqlCommand("delete student where ID=@ID", con);
            cmd.Parameters.AddWithValue("@ID", int.Parse(textBox1.Text));
            
            cmd.ExecuteNonQuery();
            con.Close();

            MessageBox.Show("Successfully Deleted"); 
        }

        private void button4_Click(object sender, EventArgs e)
        {

            SqlConnection con = new SqlConnection("Data Source=DESKTOP-MLD0RRE\\MSSQLSERVER01;Initial Catalog=CRUDForm1;Integrated Security=True;Encrypt=False");
            con.Open();
            SqlCommand cmd = new SqlCommand("select * from student where ID=@ID", con);
            cmd.Parameters.AddWithValue("@ID", int.Parse(textBox1.Text));
            SqlDataAdapter da = new SqlDataAdapter(cmd);
            DataTable dt = new DataTable(); 
            da.Fill(dt);

            dataGridView1.DataSource = dt;
        }
    }
}
