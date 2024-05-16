# .-Net-crud
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using WebApplication9.Models;
using WebApplication9.Repository;

namespace WebApplication9.Controllers
{
    public class ProductController : Controller
    {
        // GET: Product
        public ActionResult Index()
        {
            blProd obj = new blProd();
            List<Product> prodList = obj.GetProducts();
            return View(prodList);
        } 
        
        public ActionResult Create()
        {
            return View();
        }

        [HttpPost]
        public ActionResult Create(Product prod)
        {
            if (ModelState.IsValid)
            {
                blProd obj = new blProd();
                obj.InsertProduct(prod);
                return View("Index",obj.GetProducts());
            }
            return View();
        }


        public ActionResult Edit(int id)
        {
            blProd obj = new blProd();
            return View(obj.SelectById(id));
        }
        [HttpPost]
        public ActionResult Edit(Product prod)
        {
            blProd obj = new blProd();
            obj.UpdateProduct(prod);
            return View("Index", obj.GetProducts());
        }

        public ActionResult Delete(int id)
        {
            blProd obj = new blProd();
            obj.DeleteProduct(id);
            return View("Index", obj.GetProducts());
        }
    }
}




@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Create</title>
</head>
<body>
             @using(Html.BeginForm())
            {
                <table border="1" align="center">
                    <thead>
                        <tr>
                            <th colspan="2">Product Insert Form</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Enter Product Name</td>
                            <td>@Html.TextBox("prodName")
                            @Html.ValidationMessage("prodName")
                            </td>
                        </tr><tr>
                            <td>Enter Product Quantity</td>
                            <td>@Html.TextBox("prodQty")
                            @Html.ValidationMessage("prodQty")
                        </td>
                        </tr><tr>
                            <td>Enter Product Price</td>
                            <td>@Html.TextBox("prodPrice")
                            @Html.ValidationMessage("prodPrice")
                        </td>
                        </tr><tr>
                            <td>Enter Product Description</td>
                            <td>@Html.TextBox("prodDesc")
                            @Html.ValidationMessage("prodDesc")
                        </td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>
                                <button>Insert</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            }
</body>
</html>

@model WebApplication9.Models.Product
@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Edit</title>
</head>
<body>

    @using (Html.BeginForm())
    {
        <table border="1" align="center">
            <thead>
                <tr>
                    <th colspan="2">Product Update Form</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Product Id</td>
                    <td>@Html.TextBox("prodId")</td>
                </tr> <tr>
                    <td>Enter Product Name</td>
                    <td>@Html.TextBox("prodName")</td>
                </tr>
                <tr>
                    <td>Enter Product Quantity</td>
                    <td>@Html.TextBox("prodQty")</td>
                </tr>
                <tr>
                    <td>Enter Product Price</td>
                    <td>@Html.TextBox("prodPrice")</td>
                </tr>
                <tr>
                    <td>Enter Product Description</td>
                    <td>@Html.TextBox("prodDesc")</td>
                </tr>
                <tr>
                    <td></td>
                    <td>
                        <button>Update</button>
                    </td>
                </tr>
            </tbody>
        </table>
    }
</body>
</html>

[16/05, 8:32 am] Subrat Chitalo Frnd: @model WebApplication9.Models.Product
@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Edit</title>
</head>
<body>

    @using (Html.BeginForm())
    {
        <table border="1" align="center">
            <thead>
                <tr>
                    <th colspan="2">Product Update Form</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Product Id</td>
                    <td>@Html.TextBox("prodId")</td>
                </tr> <tr>
                    <td>Enter Product Name</td>
                    <td>@Html.TextBox("prodName")</td>
                </tr>
                <tr>
                    <td>Enter Product Quantity</td>
                    <td>@Html.TextBox("prodQty")</td>
                </tr>
                <tr>
                    <td>Enter Product Price</td>
                    <td>@Html.TextBox("prodPrice")</td>
                </tr>
                <tr>
                    <td>Enter Product Description</td>
                    <td>@Html.TextBox("prodDesc")</td>
                </tr>
                <tr>
                    <td></td>
                    <td>
                        <button>Update</button>
                    </td>
                </tr>
            </tbody>
        </table>
    }
</body>
</html>
 @model IEnumerable<WebApplication9.Models.Product>
@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Index</title>
</head>
<body>
   <div>
       <table align="center" border="1">
           <thead>
               <tr>
                   <th colspan="6">Product Information</th>
               </tr>
               <tr>
                   <th>Product Id</th>
                   <th>Product Name</th>
                   <th>Product Quantity</th>
                   <th>Product Price</th>
                   <th>Product Description</th>
                   <th>Actions</th>
               </tr>
           </thead>
           <tbody>
             @foreach(var item in Model)
            {
                 <tr>
                     <td>@item.prodId</td>
                     <td>@item.prodName</td>
                     <td>@item.prodQty</td>
                     <td>@item.prodPrice</td>
                     <td>@item.prodDesc</td>
                     <td>
                         @Html.ActionLink("Edit", "Edit", new {id=item.prodId}) |
                         @Html.ActionLink("Delete", "Delete", new {id=item.prodId})
                     </td>
                 </tr>
            }
           </tbody>
       </table>
       @Html.ActionLink("Create", "Create")
   </div>
</body>
</html>



using Dapper;
using System;
using System.Collections.Generic;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Web;
using WebApplication9.Models;

namespace WebApplication9.Repository
{
    public class blProd
    {
        public int InsertProduct(Product prod)
        {
            try
            {
               dlProd obj = new dlProd();
                return obj.InsertProduct(prod);
            }
            catch
            {
                return 0;
            }
        }


        public int UpdateProduct(Product prod)
        {
            try
            {
                dlProd obj = new dlProd();
                return obj.UpdateProduct(prod);
            }
            catch
            {
                return 0;
            }
        }

        public int DeleteProduct(int pid)
        {
            try
            {
                dlProd obj = new dlProd();
                return obj.DeleteProduct(pid);
            }
            catch
            {
                return 0;
            }
        }

        public List<Product> GetProducts()
        {
            try
            {
                dlProd obj = new dlProd();
                return obj.GetProducts();
            }
            catch
            {
                return null;
            }
        }

        public int CheckDuplicate(string pname)
        {
            try
            {
                dlProd obj = new dlProd();
                return obj.CheckDuplicate(pname);
            }
            catch
            {
                return -1;
            }
        }

        public Product SelectById(int pid)
        {
            try
            {
                dlProd obj = new dlProd();
                return obj.SelectById(pid);
            }
            catch
            {
                return null;
            }
        }
    }
}

using System;
using System.Collections.Generic;
using System.Configuration;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Web;
using WebApplication9.Models;
using Dapper;
namespace WebApplication9.Repository
{
    public class dlProd
    {
        public SqlConnection con;
        public dlProd() { 
            con = new SqlConnection(ConfigurationManager.ConnectionStrings["myCon"].ConnectionString);
        }

        public int InsertProduct(Product prod)
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@prodName", prod.prodName);
                parm.Add("@prodQty", prod.prodQty);
                parm.Add("@prodPrice", prod.prodPrice);
                parm.Add("@prodDesc", prod.prodDesc);
                parm.Add("@op", "Insert");
                int r = con.Execute("sp_new_product_op", parm, commandType: CommandType.StoredProcedure);
                con.Close();
                return r;
            }
            catch
            {
                return 0;
            }
        }


        public int UpdateProduct(Product prod)
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@prodId", prod.prodId);
                parm.Add("@prodName", prod.prodName);
                parm.Add("@prodQty", prod.prodQty);
                parm.Add("@prodPrice", prod.prodPrice);
                parm.Add("@prodDesc", prod.prodDesc);
                parm.Add("@op", "Update");
                int r = con.Execute("sp_new_product_op", parm, commandType: CommandType.StoredProcedure);
                con.Close();
                return r;
            }
            catch
            {
                return 0;
            }
        }

        public int DeleteProduct(int pid)
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@prodId", pid);
                parm.Add("@op", "Delete");
                int r = con.Execute("sp_new_product_op", parm, commandType: CommandType.StoredProcedure);
                con.Close();
                return r;
            }
            catch
            {
                return 0;
            }
        }

        public List<Product> GetProducts()
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@op", "Select All");
                return con.Query<Product>("sp_new_product_op", parm, commandType: CommandType.StoredProcedure).ToList();
            }
            catch
            {
                return null;
            }
        }

        public int CheckDuplicate(string pname)
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@op", "Check DProd");
                parm.Add("@prodName", pname);
                List<Product> list = con.Query<Product>("sp_new_product_op", parm, commandType: CommandType.StoredProcedure).ToList();
                if (list.Count > 0)
                {
                    return 1;
                }
                return 0;
            }
            catch
            {
                return -1;
            }
        }
        
        public Product SelectById(int pid)
        {
            try
            {
                if (con.State != ConnectionState.Open)
                {
                    con.Open();
                }
                DynamicParameters parm = new DynamicParameters();
                parm.Add("@op", "Select One");
                parm.Add("@prodId", pid);
                Product prod = con.Query<Product>("sp_new_product_op", parm, commandType: CommandType.StoredProcedure).ToList().FirstOrDefault();
                return prod;
            }
            catch
            {
                return null;
            }
        }


    }
}
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Web;

namespace WebApplication9.Models
{
    public class Product
    {
        [Key]
        public int prodId { get; set; } = 0;
        [Required(ErrorMessage ="Please Enter Product Name"),MaxLength(20,ErrorMessage ="Product Name Too Long..!")]
        public string prodName { get; set; } = null;
        [Required(ErrorMessage ="Please Enter Product Quatinty")]
        [Range(1,20,ErrorMessage ="Quantity must be 1 to 20")]
        public int prodQty { get; set; } = 0;
        [Required(ErrorMessage ="Please Enter Product Price")]
        public double prodPrice { get; set; } = 0.0;
        [Required(ErrorMessage ="Please Enter Product Description")]
        public string prodDesc { get; set; } = null;
    }
}
