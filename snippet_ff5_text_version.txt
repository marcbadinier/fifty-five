clear();
var listProdView = []; var found = false;
//  Fill function () : for each item in array (selected by class 'product-container'), if the item is in viewport -> if the item is not found into the viewed list's array : add item to array & console.
function fillConsole(){ Array.from(document.getElementsByClassName("product-container")).forEach(function(item) {
    if( item.getBoundingClientRect().bottom > 0 && window.innerHeight - item.getBoundingClientRect().bottom > 0){//todo ici
        for(let i = 0; i < listProdView.length; i++) { if (listProdView[i] == (item.outerText.replace(/[\n\r]+/g, ' ')).replace('EXCLU WEB ', '')) {found = true;} }
        if (!found){ console.log((item.outerText.replace(/[\n\r]+/g, ' ')).replace('EXCLU WEB ', '')); listProdView.push((item.outerText.replace(/[\n\r]+/g, ' ')).replace('EXCLU WEB ', '')); }
        found = false; } } ); }
//  first load
fillConsole();
//   Event : scrolling
window.addEventListener('scroll', function(e) { fillConsole() });