# Jquery-Ajax-to-.Net-MVC-Server
Jquery AJAX to communicate with .Net MVC controller and Parse returned JSON


```
// Ajax to server to get data
            
            $.ajax({

                xhr: function () {
                    var progress = $('.progress'),
                        xhr = $.ajaxSettings.xhr();

                    progress.show();

                    xhr.upload.onprogress = function (ev) {
                        if (ev.lengthComputable) {
                            var percentComplete = parseInt((ev.loaded / ev.total) * 100);
                            progress.val(percentComplete);
                            if (percentComplete === 100) {
                                progress.hide().val(0);
                            }
                        }
                    };

                    return xhr;
                },


                type: 'GET',
                url: '/Controller/getdata?dataid=' + dataid,
                dataType: 'text',
                success: function (data) {
                    //alert(data);
                    var json_obj = $.parseJSON(data);//parse JSON                    
                    $("#divshowresults").text('Data: ' + json_obj.thedatafield1 + ' / ' + json_obj.thedatafield2);                   
                    $('.loading-overlay').hide();
                },
                error: function (emp) {
                    alert('error sending to MVC controller');
                    $('.loading-overlay').hide();
                }
            });

```

the MVC .Net Controller codes looks like

```
public async Task<DataResults> getData(float Dataid)
        {
            var Result = new DataResults(); 
            
            // you can do something with the dataid DATA that querystring contains
            
            Result.thedatafield1 = 'some data';
            Result.thedatafield2 = 'some more data';

            return Result
}

Public class DataResults
{
            public string thedatafield1;
            public string thedatafield2;
}
```
