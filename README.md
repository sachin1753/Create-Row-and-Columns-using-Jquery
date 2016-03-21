# Create-Row-and-Columns-using-Jquery
It related to the jQuery,
If I will say, Create dynamic row and columns using jQuery or javascript. it's look eassay but took lots of our time to impliment the same. 
I implimented once that feature and feel like I need to share this with all to save others time.

We need to follow the following steps like:

Create Textbox with following class and name:
class="dynamicRow" name="data[add][row'+j+']"
class="dynamicCol" name="data[add][columns'+j+']"
Like
//creating row and columns
$c[] = form_element_wrap(form_text('dyCol', '', 'dynamic-columns'), '', 'Columns');
$c[] = form_element_wrap(form_text('dyRow', '', 'dynamic-rows'), '', 'Rows');
$c[] = '<div id="dynamic-structure" class="div-table"></div>'; 

Script to handle text boxes:
jQuery('#dyCol, #dyRow ').on('keyup',function(event) {
                                MFOPADMIN.user.createCol(event);
                        });

// ! MFOPADMIN.user.createCol
		createCol: function(){
                    var defaultRow='';
                    var newCol='';
                    var numCol = jQuery('#dyCol').val();
                    var numRow = jQuery('#dyRow').val();
                    if(jQuery('#dyRow').length){
                        var oldRow = jQuery('#dynamic-structure').children('div').length;
                        if(oldRow < numRow)
                        {
                            for (var i = oldRow; i < numRow; i++) {
                                defaultRow = '<div class="div-table-row row-count'+i+'"></div>';
                                jQuery("#dynamic-structure").append(defaultRow);
                                var oldCol = jQuery('.row-count'+i).children('div').length;
                                if(oldCol < numCol)
                                {
                                    for (var j = oldCol; j < numCol; j++) {
                                        if(i==0){
                                            newCol = '<div class="div-table-col col-count'+j+'"><input type="text" name="column['+j+']" size="10" /></div>';
                                        }else{
                                            if(j==0){
                                                newCol = '<div class="div-table-col col-count'+j+'"><input type="text" name="row['+j+']" size="10" /></div>';
                                            }else{
                                                newCol = '<div class="div-table-col col-count'+j+'">&nbsp;</div>';
                                            }
                                        }
                                        jQuery(".row-count"+i).append(newCol);
                                    }
                                }                        
                            }
                        }else{
                            if(oldRow > numRow)
                            {
                                var remRowDIV = (oldRow-numRow);
                                $('#dynamic-structure > .div-table-row').slice(-remRowDIV).remove();
                            }
                            if(oldRow == numRow)
                            {
                                oldRow=0;
                                for (var i = oldRow; i < numRow; i++) {
                                    var oldCol = jQuery('.row-count'+i).children('div').length;
                                    if(oldCol < numCol){
                                        for (var j = oldCol; j < numCol; j++) {
                                            if(i==0){
                                                newCol = '<div class="div-table-col col-count'+j+'"><input type="text" name="column['+j+']" size="10" /></div>';
                                            }else{
                                                if(j==0){
                                                    newCol = '<div class="div-table-col col-count'+j+'"><input type="text" name="row['+j+']" size="10" /></div>';
                                                }else{
                                                    newCol = '<div class="div-table-col col-count'+j+'">&nbsp;</div>';
                                                }
                                            }
                                            jQuery(".row-count"+i).append(newCol);
                                        }
                                    }                        
                                    if(oldCol > numCol){
                                        var remColDIV = (oldCol-numCol);
                                        console.log('.row-count'+i+' > div-table-col');
                                        $('.row-count'+i+' > .div-table-col').slice(-remColDIV).remove();
                                    }

                                }
                            }                        
                        }
                    }
                    else
                    {
                        if(!jQuery('.row-count0').length)
                        {
                            defaultRow = '<div class="div-table-row row-count0"></div>';
                            jQuery("#dynamic-structure").append(defaultRow);
                        }
                        var oldCol = jQuery('.row-count0').children('div').length;
                        if(oldCol < numCol)
                        {
                            for (var i = oldCol; i < numCol; i++) {
                                newCol = '<div class="div-table-col col-count'+i+'"><input type="text" name="column['+i+']" size="10" /></div>';
                                jQuery(".row-count0").append(newCol);
                            }
                        }
                        if(oldCol > numCol)
                        {
                            var remDIv = (oldCol-numCol);
                            $('.row-count0 > .div-table-col').slice(-remDIv).remove();
                        }
                    }
		},


