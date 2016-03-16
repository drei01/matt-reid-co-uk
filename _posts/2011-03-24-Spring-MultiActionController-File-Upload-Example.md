---
layout: post
title: Spring MultiActionController File Upload Example
---

I have been working on a Spring MVC web app that needed to accept a
multi-part file upload (an excel file in this case). There are plenty of
examples of handling file uploads with Spring but I couldn't find a
concrete example for a web app that was using a
[MultiActionController](http://static.springsource.org/spring/docs/3.0.x/api/org/springframework/web/servlet/mvc/multiaction/MultiActionController.html)
and to change the controller on the app would have taken a while. After
some trial and error I found a solution so here it is.

Application Context
-------------------

In your application context you must have a multipart resolver in order
to allow successful file uploads from a form. Add the following XML

``` {.js name="code"}
        
     
```

File Upload Bean
----------------

Next we need to define a bean which our uploaded file will be bound to.
Create the following class.

``` {.js name="code"}
public class FileUploadBean {
    private MultipartFile file;

    public MultipartFile getFile() {
        return file;
    }

    public void setFile(MultipartFile file) {
        this.file = file;
    }
}
```

The Form
--------

In a new **jsp** add the following Spring form in order to bind the file
with the correct name

``` {.js name="code"}
 
            
                Choose file

                
            
            
                
                        
        
```

Controller
----------

In the MultipartController for your web app, add the following methods,
to display the form:

``` {.js name="code"}
public ModelAndView fileUpload (HttpServletRequest request, HttpServletResponse response){
        ModelAndView mav = new ModelAndView("embargoDate/fileUpload");
        mav.addObject("file", new FileUploadBean());
        return mav;
    }
```

*note that we add a new File bean into the model and view so that it can
be bound by the form*

To process the form we need the following method.:

``` {.js name="code"}
public ModelAndView submitFileUpload (HttpServletRequest request, HttpServletResponse response, FileUploadBean file) {
        if(file==null){
            logger.error("the file uploaded is null, something went wrong");
            return null;
        }

        try {
            POIFSFileSystem fileSystem = null;          
            try{//get the excel document
                fileSystem = new POIFSFileSystem(new ByteArrayInputStream(file.getFile().getBytes()));
            }catch (Exception e) {
                logger.error("The file uploaded is not an excel file");
                return null;
            }
            HSSFWorkbook workBook = new HSSFWorkbook (fileSystem);
            HSSFSheet sheet = workBook.getSheetAt (0);
            Iterator rows = sheet.rowIterator();

            //for each row in the spreadsheet
            while (rows.hasNext()){
                Row row = rows.next();

                // display row number in the console.
                System.out.println ("Row No.: " + row.getRowNum ());

                // once get a row its time to iterate through cells.
                Iterator cells = row.cellIterator();

                while (cells.hasNext ()){
                    Cell cell = cells.next();

                    System.out.println ("Cell No.: " + cell.getColumnIndex());

                    /*
                     * Now we will get the cell type and display the values
                     * accordingly.
                     */
                    switch (cell.getCellType ()){
                        case HSSFCell.CELL_TYPE_NUMERIC :
                        {                       
                            // cell type numeric.
                            System.out.println ("Numeric value: " + cell.getStringCellValue());                     
                            break;
                        }

                        case HSSFCell.CELL_TYPE_STRING :
                        {                       
                            // cell type string.
                            RichTextString richTextString = cell.getRichStringCellValue ();

                            System.out.println ("String value: " + richTextString.getString ());

                            break;
                        }

                        default :
                        {                           
                            // types other than String and Numeric.
                            System.out.println ("Type not supported.");

                            break;
                        }
                    }
                }
            }

        } catch (IOException e) {
            logger.error("error reading excel file",e);
        }

        return new ModelAndView("returnPage");
    }
```

Note that my method is using [Apache POI](http://poi.apache.org/) to
process an Excel file by you can do anything that you like with the file
that is uploaded.

You should now be ready to upload and process files in your Spring
MultiActionController.

Enjoy,

Matt

 









