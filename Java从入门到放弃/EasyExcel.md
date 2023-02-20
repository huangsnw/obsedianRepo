```java
public void eventExport(String ids, HttpServletResponse response, Integer type) throws IOException { 
	/* 设置返回response结构 */ 
	response.setContentType("application/vnd.ms-excel"); 
	response.setCharacterEncoding("UTF-8"); 
	/* 车辆进出导出 */ 
	if (type == 0) { 
	/* 下载文件的名字 */ 
	String fileName = URLEncoder.encode("车辆进出导出", "UTF-8").replaceAll("\\+", "%20"); 
	response.setHeader("Content-disposition", "attachment;filename*=utf-8''" + fileName + ".xlsx"); 
	/* 车辆数据List */ 
	List<VehicleEventExport> data = new ArrayList<>(); 
	/* 分别从数据库拿到车辆事件数据 */ 
	for (String s : ids.split(ServiceConstant.COMMA)) { 
		data.add(eventMapper.exportVehicle(s)); 
	} 
	EasyExcel.write(response.getOutputStream(), VehicleEventExport.class) .sheet("sheet1") .doWrite(data); 
}
```