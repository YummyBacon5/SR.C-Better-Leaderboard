// ==UserScript==
// @name         SR.C Better Leaderboard
// @namespace    https://github.com/YummyBacon5
// @version      1.0.0
// @description  This shows all hidden variables, removes the sub-category dropdowns and display all the categories at once!
// @author       Yummy_Bacon5
// @match        https://www.speedrun.com/*
// @icon         https://drive.google.com/uc?id=1evLQo0tDq48SnI_tLlXEeofU_kQ5Mcbd&export=download
// @homepageURL  https://github.com/YummyBacon5/SR.C-Better-Leaderboard
// @downloadURL  
// @updateURL    
// ==/UserScript==

(function() {
    "use strict";

    function getElementsStartsWithId(id) {
        var all = document.body.getElementsByTagName("*"), elements = []
        for(let i = 0; i < all.length; i++) {
            if(all[i].id.substr(0, id.length) == id) {
                elements.push(all[i])
            }
        }
        return elements
    }

    //Removes the dropdowns from sub-categories
    const subCategories = document.querySelectorAll(".dropdown.variable")
    for(let i = 0; i < subCategories.length; i++) {
        const subCategory = subCategories[i], subCategoryChildren = subCategory.children
        subCategory.className = "btn-group custom-radio-group variable"
        subCategory.innerHTML = subCategoryChildren[1].innerHTML
        for(let j = 0; j < subCategoryChildren.length; j++) {
            const child = subCategoryChildren[j]
            child.className = "btn btn-default variable-tab"
            if(child.tagName != "A") {
                continue
            }
            const replacement = document.createElement("label")
            for(let tagIndex = 0; tagIndex < child.attributes.length; tagIndex++) {
                replacement.setAttribute(child.attributes.item(tagIndex).nodeName, child.attributes.item(tagIndex).nodeValue)
            }
            replacement.innerHTML = child.innerHTML
            child.parentNode.replaceChild(replacement, child)
        }
    }

    //When the dots appear we exacute the unhideVariables() function
    setInterval(() => {
        if(document.getElementsByClassName("hidden-variables")) {
            //This unhides all of the hidden variables
            const hiddenVariables = document.querySelectorAll(".hidden-variables")
            for(let i = 0; i < hiddenVariables.length; i++) {
                const hidden = hiddenVariables[i]
                for(let j = 0; j < hidden.children.length; j++) {
                    const hiddenChild = hidden.children[j]
                    let name = `<th class="hidden-lg-down variable-column">${hiddenChild.innerHTML}</th>`
				if(i != 0) {
                    name = `<td class="nobr center hidden-xs hidden-lg-down">${hiddenChild.querySelector("span").innerHTML}</td>`
				}
                hidden.parentNode.insertAdjacentHTML("beforebegin", name)
            }
            hidden.parentNode.remove()
        }
        }
    }, 100);

    //Checks if the miscellaneous tab is null to not cause erros
    const miscElement = document.getElementById("miscellaneous")
    if(miscElement) {
        miscElement.style.display = "block"
    }
    //Displays all the categories in the old style
    const catElements = getElementsStartsWithId("category")
    for(let i = 0; i < catElements.length; i++) {
        catElements[i].style.display = "block"
    }
    //Removes the category arrows
    const caretElements = getElementsStartsWithId("pending-caret")
    for(let i = 0; i < catElements.length; i++) {
        caretElements[i].style.display = "none"
    }
})();
