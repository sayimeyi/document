package move;

import java.io.File;
import java.util.Vector;

public class MoveFile {

	private Vector<String> ver =new Vector<String>();
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub

		MoveFile moveFile = new MoveFile();
		moveFile.move();
	}
	
	public void move() {
		String path = "C:\\testMovefile\\springboot2-jpa-crud-example";
		ver.add(path);
        while(ver.size()>0){
            File[] files = new File(ver.get(0).toString()).listFiles();    
            ver.remove(0);
            
            for(File file:files){
                String tmp=file.getAbsolutePath();
                if(file.isDirectory()){
                	ver.add(tmp);
                }else {
                	
                	String fileName = file.getName();
                	System.out.println(file.getAbsolutePath());
                	String folder = "dummy";
                    if (fileName.contains(".")) {
                		
                		 folder = fileName.substring(fileName.lastIndexOf(".")+1,fileName.length());
                	}
                    folder = "C:\\testMovefile\\testFolder1\\"+
                    		folder+File.separator;
//                	System.out.println(folder);
                	File folderFile = new File (folder);
                	if(!folderFile.exists()) {
                		folderFile.mkdir();
                	}
                	file.renameTo(new File (folder+file.getName()) );
                }    

            }
        }

	}

}
