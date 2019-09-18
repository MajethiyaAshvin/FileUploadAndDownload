# FileUploadAndDownload


	@RequestMapping(value = "/upload", method = RequestMethod.POST, consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
	public String fileUpload(@RequestParam("file") MultipartFile file) throws IOException {
		File convertFile = new File("/var/tmp/" + file.getOriginalFilename());
		convertFile.createNewFile();
		FileOutputStream fout = new FileOutputStream(convertFile);
		fout.write(file.getBytes());
		fout.close();
		return "File is upload successfully";
	}

	@RequestMapping(value = "/download", method = RequestMethod.GET)
	public ResponseEntity<Object> downloadFile() throws IOException {
		String filename = "/var/tmp/HELP.md";
		File file = new File(filename);
		InputStreamResource resource = new InputStreamResource(new FileInputStream(file));
		HttpHeaders headers = new HttpHeaders();

		headers.add("Content-Disposition", String.format("attachment; filename=\"%s\"", file.getName()));
		headers.add("Cache-Control", "no-cache, no-store, must-revalidate");
		headers.add("Pragma", "no-cache");
		headers.add("Expires", "0");

//		ResponseEntity<Object> responseEntity = ResponseEntity.ok().headers(headers).contentLength(file.length())
//				.contentType(MediaType.parseMediaType("application/txt")).body(resource);
//		return responseEntity;
//		
//		
		
		return new ResponseEntity<>("Dounload Successes..........?",HttpStatus.OK);
		
	}












