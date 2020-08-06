# GoStarWeb
**GoStar微服务框架之微型WEB开发组件框架**

**GoStar微服务重要组成部分，可以无缝迁移其他WEB框架**

*支持路由控制*
*支持中间件*
*支持错误控制*

*使用说明*

`type student struct {
 	Name string
 	Age  int8
 }
 
 func formatAsDate(t time.Time) string {
 	year, month, day := t.Date()
 	return fmt.Sprintf("%d-%02d-%02d", year, month, day)
 }
 
 func main() {
 	r := GoStarWeb.New()
 	r.Use(GoStarWeb.Logger())
 	r.SetFuncMap(template.FuncMap{
 		"formatAsDate": formatAsDate,
 	})
 	r.LoadHTMLGlob("templates/*")
 	r.Static("/assets", "./static")
 
 	stu1 := &student{Name: "GoStarWeb", Age: 20}
 	stu2 := &student{Name: "GoStar", Age: 22}
 	r.GET("/", func(c *GoStarWeb.Context) {
 		c.HTML(http.StatusOK, "css.tmpl", nil)
 	})
 	r.GET("/students", func(c *GoStarWeb.Context) {
 		c.HTML(http.StatusOK, "arr.tmpl", GoStarWeb.H{
 			"title":  "GoStarWeb",
 			"stuArr": [2]*student{stu1, stu2},
 		})
 	})
 
 	r.GET("/date", func(c *GoStarWeb.Context) {
 		c.HTML(http.StatusOK, "custom_func.tmpl", GoStarWeb.H{
 			"title": "GoStarWeb",
 			"now":   time.Date(2019, 8, 17, 0, 0, 0, 0, time.UTC),
 		})
 	})
 
 	r.Run(":9999")
 }`
