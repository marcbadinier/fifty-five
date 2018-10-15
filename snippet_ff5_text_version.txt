//https://www.leslipfrancais.fr/maillots-de-bain-326
//redirect
//https://www.leslipfrancais.fr/maillots-de-bain-homme-326


//  Choose debug level mode for console
//var debugMode = true
var debugMode = false

//  Clear console
console.clear()

console.log("_ - Console Messages - Debug level mode set to : " + debugMode.toString().toUpperCase())

//  Get the url
currentUrl = window.location.href
//currentUrl = document.URL

if(currentUrl.toLowerCase() != "https://www.leslipfrancais.fr/maillots-de-bain-homme-326")
{
    console.log("\n0 - Cette page n'est pas compatible pour ce snippet !\nUtilisez la page suivante : https:\/\/www.leslipfrancais.fr\/maillots-de-bain-326")
}
else
{
    console.log("\n0 - Cette page est compatible pour ce snippet.")
    //  Declare HTMLCollection object for class 'product-name'
    let htmlCollecProductName = document.getElementsByClassName("product-name")
    //  Verify object's content
    debugMode && console.log("\n1 - Content of htmlCollecProductName :")
    debugMode && console.log(htmlCollecProductName)

    //  Verify object's length : must be the complete list of products
    debugMode && console.log("\n2 - Number of product : " + (htmlCollecProductName.length -1))                 

    //  Verify the first entry's title - The [0] element is not a good entry for this list
    let theName = htmlCollecProductName[1].getAttribute("title")
    debugMode && console.log("\n3 - Product Name [element 1] : " + theName)

    //    -----   Navigate into DOM (parent nodes then new childs)    -----

    //  Declare HTMLCollection object for class 'product-price'
    let htmlCollecProductPrice = htmlCollecProductName[1].parentNode.parentNode.parentNode.getElementsByClassName("product-price")
    debugMode && console.log("\n4 - Content of htmlCollecProductPrice :")
    debugMode && console.log(htmlCollecProductPrice)

    //  Verify object's length : must be the only first one
    debugMode && console.log("\n5 - Number of product : " + htmlCollecProductPrice.length)

    //  Declare currency var to work with it (if necessary : split, change, keep price in float format,...) 
    let currency = "€"

    //  Work with pos into string to keep only the price
    let currencyPos = htmlCollecProductPrice[0].innerText.indexOf(currency)

    //  Verify the price into float format
    debugMode && console.log("\n6 - Price's product : " + htmlCollecProductPrice[0].innerText.slice(0, currencyPos - 1) + " " + currency)
    let thePrice = htmlCollecProductPrice[0].innerText.slice(0, currencyPos - 1)

    //  Loop into htmlCollecProductName to shwo product name and associated price
    debugMode && console.log("\n7 - Loop into htmlCollecProductName")
    if (debugMode)
    {
        for(let i = 1; i < htmlCollecProductName.length; i++)
        {
            htmlCollecProductPrice = htmlCollecProductName[i].parentNode.parentNode.parentNode.getElementsByClassName("product-price")
            currencyPos = htmlCollecProductPrice[0].innerText.indexOf(currency)
            thePrice = htmlCollecProductPrice[0].innerText.slice(0, currencyPos - 1)
            console.log("Product Name [element " + i + "] : " + htmlCollecProductName[i].getAttribute("title") + " / Price : " + thePrice + " " + currency) 
        }
    }
    //  Loop into htmlCollecProductName to create an array list
    //  of product name and associated price (instead of a classical array)
    debugMode && console.log("\n8 - Loop before load values into listProductPrice, to verify future entries")
    let listProductPrice = [];
    for(let i = 1; i < htmlCollecProductName.length; i++)
    {
        if (debugMode)
        {
            htmlCollecProductPrice = htmlCollecProductName[i].parentNode.parentNode.parentNode.getElementsByClassName("product-price")
            theName = htmlCollecProductName[i].getAttribute("title")
            currencyPos = htmlCollecProductPrice[0].innerText.indexOf(currency)
            thePrice = htmlCollecProductPrice[0].innerText.slice(0, currencyPos - 1)  

            //  Verify each result into the loop
            debugMode && console.log("Product Name [element " + i + "] : " + htmlCollecProductName[i].getAttribute("title") + " / Price : " + thePrice + " " + currency) 

        //  Fill the list with each result's line
        listProductPrice.push({ name: `${theName}`, price: `${thePrice}` })
        }
    }

    //  Verify listProductPrice's content
    debugMode && console.log("\n9 - Values into listProductPrice")
    if (debugMode)
    {
        for(let indice in listProductPrice)
        {
            debugMode && console.log("Product Name [element " + (parseInt(indice) + 1) + "] : " + listProductPrice[indice].name + " / Price : " + listProductPrice[indice].price + " " + currency)
        }
    }

    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    //  Main
    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    var listProductPriceView = [];
    var entryFound = false

    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    function showResult()
    {
      try
      {
        if (!debugMode)
        {
            console.clear()
        }    

        console.log("Values into listProductPriceView")
        console.log("--------------------------------")
        for(let indice in listProductPriceView)
        {
            console.log("Product Name [element " + (parseInt(indice) + 1) + "] : " + listProductPriceView[indice].name + " / Price : " + listProductPriceView[indice].price + " " + currency)
        }       
      }
      catch(error)
      {
        console.log(error);
      }
    }


    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    function fillArrayOfVisibleInViewportOnce()
    {
      try
      {
        //  For each element in product list array
        for (let i = 1; i < htmlCollecProductName.length; i++)
        {
            //  Check if container's bottom are in the viewport.
            //  Possible to check top & bottom for more precision here...or another parent's div ...
            debugMode && console.log(".bottom : " + htmlCollecProductName[i].getBoundingClientRect().bottom)
            if( htmlCollecProductName[i].getBoundingClientRect().bottom > 0)
            {
                var prov = window.innerHeight - htmlCollecProductName[i].getBoundingClientRect().bottom
                debugMode && console.log(prov)
            }

            //  The getBoundingClientRect() and viewport result doesn't work correctly on chrome in this case !.
            //  Using window.innerHeight also.
            if( htmlCollecProductName[i].getBoundingClientRect().bottom > 0 &&
                window.innerHeight - htmlCollecProductName[i].getBoundingClientRect().bottom > 0)
            {
                debugMode && console.log("Object is in viewport.")

                htmlCollecProductPrice = htmlCollecProductName[i].parentNode.parentNode.parentNode.getElementsByClassName("product-price")
                theName = htmlCollecProductName[i].getAttribute("title")

                //  If product is not already in the list, add it
                for(let i = 0; i < listProductPriceView.length; i++)
                {
                    if (listProductPriceView[i].name == theName)
                    {
                        entryFound = true
                        i = listProductPriceView.length
                    }
                }
                if (!entryFound)
                {
                    currencyPos = htmlCollecProductPrice[0].innerText.indexOf(currency)
                    thePrice = htmlCollecProductPrice[0].innerText.slice(0, currencyPos - 1)
                    listProductPriceView.push({ name: `${theName}`, price: `${thePrice}` })
                }
                else
                {
                    entryFound = false
                }
            }        
            else
            {
              debugMode && console.log("Object is out of viewport.")
              //  Nothing TODO
            }
        }
      } 
      catch(error)
      {
        console.log(error);
      }
    }
    
    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    //  First call, load page
    fillArrayOfVisibleInViewportOnce()

    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    //  Verify listProductPrice's content
    showResult()

    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
    //  Traitement dans l'event scrolling
    window.addEventListener('scroll', function(e)
    {
      try
      {  
        //  Remenber the first elem of [htmlCollecProductName] is not a product card...
        if(listProductPriceView.length != htmlCollecProductName.length - 1)
        {
            fillArrayOfVisibleInViewportOnce()
            //  Verify listProductPrice's content
            //  If in debug mode
            debugMode && console.log("\n11 - Values into listProductPriceView")
            //  In final release mode
            showResult()
        }
        else
        {
            //  No more action TODO
            debugMode && console.log("Scan Complete !")            
        }
      }
      catch(error)
      {
        console.log(error);
      }      
    });
    //*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
}

