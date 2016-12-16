# autocmplet
/*......................short code for auto cmplt...............*/
 
 $("#searchForm").submit(function(){
   
    selectedUrl = $('.searchresult ul li.selected a').attr('href');
    if(typeof selectedUrl != 'undefined'){
     window.location = selectedUrl;
     return false;
    }
    else
     return true;
   });
     var displayBoxIndex = -1;
   var Navigate = function (diff) {
    displayBoxIndex += diff;
    var oBoxCollection = $(".searchresult ul li");
    if (displayBoxIndex >= oBoxCollection.length) {
     displayBoxIndex = 0;
    }
    if (displayBoxIndex < 0) {
     displayBoxIndex = oBoxCollection.length - 1;
    }
    var cssClass = "selected";
    oBoxCollection.removeClass(cssClass).eq(displayBoxIndex).addClass(cssClass);
   }

   $("#search").on("keyup", function(e) {

    if (e.keyCode == 40) {
     //down arrow
     Navigate(1);
     //return false;
    }
    if (e.keyCode == 38) {
     //up arrow
     Navigate(-1);
     //return false;
    }
   
    //$(".searchresult ul").html('');
    if (e.keyCode >= 65 && e.keyCode <= 90 || e.keyCode >= 97 && e.keyCode <= 122 || 8 == e.keyCode || 190 == e.keyCode ) {
     $(".searchresult ul").html('');
     var searchTerm = $("#search").val();
     $.ajax({
      type: "GET",
      url: base_url + "common/getStoreByName",
          dataType: "json",
      data: {query : searchTerm},
      success: function(e) {
       $(".searchresult ul").html('');
       for(var i=0; i<e.length; i++){
        $(".searchresult ul").append("<li><a href='"+base_url+e[i]['id']+"'>"+e[i]['name']+"</a><a class='recordtype' href=''>Website</a></li>");
       }
       $('.searchresult').addClass('active');
       $('.searchresult li').first().addClass('selected');
      },
      error : function(){
       //alert("som  error ");
      },
     });
    }
    
   
    // if($('.srchinput').val() == ''){
    //  $('.searchresult').removeClass('active');
    // }
      });
   /*search end*/
