var outer_quote = document.getElementsByClassName("post-body")[0].getElementsByTagName("div");
for (i = 0; i < outer_quote.length; i++)
{
	if (outer_quote[i].innerHTML.search("#صف") != -1)
	{
		outer_quote[i].setAttribute("id", "outer_page")
	}
}
if (document.getElementById("outer_page") != undefined)
{
	var outer_page_element = document.getElementById("outer_page_cont");
	var outer_page = document.getElementById("outer_page");
	$("#outer_page").replaceWith("<center><br/><div id='outer_page_btn' onclick='open_outer_page()'>&#11015; عرض روابط التحميل &#11015;</div><br/></center>");
	$("#outer_replace_part").replaceWith("<div id='outer_table'><div id='t_timer'>فضلا&#1611; أنتظر ...</div><div class='t_off'>" + outer_page.innerHTML + "</div></div>")
}
var x_timer = 5;

function begin_timer()
{
	var t_interval = setInterval(function ()
	{
		if (x_timer < 1)
		{
			clearInterval(t_interval);
			var outer_table = document.getElementById("outer_table");
			var outer_table_cont = outer_table.innerHTML;
			var outer_table_cont_array = outer_table_cont.split("*");
			var no_of_lines = outer_table_cont_array.length / 5;
			var t_txt = "";
			for (i = 0; i < no_of_lines; i++)
			{
				var t_x = outer_table_cont.split("#صف")[i + 1];
				var t_y = t_x.split("*");
				t_txt += "<tr><td class='t_title'>" + t_y[1] + "</td><td class='t_version'>" + t_y[3] + "</td><td class='t_size'>" + t_y[2] + "</td><td class='t_download'>" + t_y[4] + "</td></tr>"
			}
			document.getElementById("outer_table").innerHTML = "<center><table id='outer_page_table'><tr><th>اسم الملف</th><th>ملحوظة</th><th>حجم الملف</th><th>روابط التحميل</th></tr>" + t_txt + "</table></center>";
			document.getElementById("outer_page_table").style.display = "inline-table";
			$("#outer_page_table br").replaceWith("")
		}
		document.getElementById("t_timer").innerHTML = x_timer;
		x_timer--
	}, 1e3)
}

function close_outer_page()
{
	outer_page_element.classList.remove("outer_page_cont")
}

function open_outer_page()
{
	outer_page_element.setAttribute("class", "outer_page_cont");
	begin_timer()
}
