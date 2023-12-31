
<%*
// Check the folder specified below and build a list of all markdown files
// all files in subfolders will be included

// = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
// MacOS example
folderChoicePath = "Templates/"
// If you are on Windows, try: "resources\health\"
// Note: "/" works fine under Windows 10
// = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =

if (folderChoicePath != null) {
	new Notice(`Folder: ${folderChoicePath}`, 5000);
	let filesInFolder = new Array();
	let headings = new Array();
	console.log("folderChoicePath: " + `${folderChoicePath}`)
	filesInFolder =  app.vault.getMarkdownFiles().filter(file => file.path.includes(folderChoicePath)).map(tFile=>tFile.basename)
	const filesList = new Array();
	filesList.push('\n| Template | Description | Detailed Notes |\n| -------- | ----------- | -------------- |')
	filesInFolder.forEach((file) => {
		filesList.push('\n|[[' + file + ']] | - | [[#' + file + ']] |')
		headings.push('\n## ' + file + '\n')
	});
	const folderChoice = folderChoicePath.split("/").slice(-2).join("")
	const fileName = folderChoice + " MOC"
	//files sorted case insensitive
	const heading = "## " + folderChoice.charAt(0).toUpperCase() + folderChoice.slice(1)+ " MOC"
	let content = heading + "\n" + filesList.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase())).join('')
	content = content + "\n" + headings.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase())).join('')

	// insert the list of files in the active file
	tR+=content
	new Notice(`Created new MOC`, 5000);	
} else {
	new Notice(`No folder selected`, 5000);
}
_%>
