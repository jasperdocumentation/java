# java
Jasper reports for Java program. Has an example.

	public void makeReport(HttpServletResponse response, int id) throws Exception{
		Bank bank = br.getOne(id);
		List<Account> allAccs = bank.getAccounts();
		//Collections.sort(allAccs, new Comparator());
		response.setContentType("text/html");
		JRBeanCollectionDataSource dataSource = new JRBeanCollectionDataSource(allAccs);
		InputStream inputStream = this.getClass().getResourceAsStream("/jasperreports/repost.jrxml");
		JasperReport jasperReport = JasperCompileManager.compileReport(inputStream);
		Map<String, Object> params = new HashMap<String, Object>();
		params.put("date", bamk.getDate());
		params.put("name", bank.getName());
		params.put("number", bank.getNumber());
		JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, params,dataSource);
		inputStream.close();

		response.setContentType("application/x-download");
		response.addHeader("Content-disposition", "attachment; filename=JReport.pdf");
		OutputStream out = response.getOutputStream();
		JasperExportManager.exportReportToPdfStream(jasperPrint, out);
	}
