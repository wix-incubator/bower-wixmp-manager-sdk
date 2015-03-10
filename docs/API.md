# API

* wixmp

* wixmp.events (see [events.md](events.md))
* wixmp.events.on(eventName, listener(promise, EventObject))
* wixmp.events.off(eventName, listener)

* wixmp.bi(state{boolean}) {function}

* wixmp.connectExternalSource(source{Source})

* wixmp.sources{object}

* wixmp.Source(sourceConstructor{function}, sourceConfig{object}) -> source{Source}

* Source

* Source.name{string}

* Source.folders
* Source.folders.list(folderId) -> promise resolved with List of Folder
* Source.folders.remove(ids) -> array of promise 

* Source.folder
* Source.folder.create(folderName) -> promise resolved with Folder
* Source.folder.update(folder, diff{object}) -> promise resolved with modified Folder

* Source.items
* Source.items.list(folderId, options{ListOptions}) -> promise resolved with List of Item
* Source.items.search(folderId, query, options{ListOptions}) -> promise resolved with List of Item
* Source.items.remove(itemIds) -> array of promise
* Source.items.upload(files, options) -> array of promise
* Source.items.uploadByUrl(files, options) -> array of promise

* Source.item
* Source.item.get(itemId) -> promise with resolved Item
* Source.item.update(item, diff{object}) -> promise resolved with modified Item

## Objects

* ListOptions
* ListOptions.paging{object}
* ListOptions.paging.cursor{string}
* ListOptions.paging.pageSize{number}
* ListOptions.sort{object}
* ListOptions.sort.order{string}
* ListOptions.sort.field{string}

* List
* List.data{array}
* List.paging{object}

* File
* File.mediaType{string}
* File.size{number}
* File.name{string}
* File.file{File}
* File.url{string}
* File.tags{array}

* Item
* Item.id{string}
* Item.folderId{string}          
* Item.name{string}              
* Item.mediaType{string}         
* Item.fileUrl{string}           
* Item.thumbnailUrl{string}      
* Item.originalUrl{string}       
* Item.previewUrl{string}        
* Item.sampleUrl{string} // deprecated
* Item.createdAt{date}         
* Item.tags{array}              
* Item.width{number}             
* Item.height{number}             
* Item.fileInfo{object} // deprecated          
* Item.fileInput{object}         
* Item.fileOutput{object}
* Item.transcodingStatus{string}
* Item.duration{number}

* Folder
* Folder.id{string}      
* Folder.name{string}      
* Folder.mediaType{string}
* Folder.filesCount{number}
* Folder.createdAt{date}

* EventObject
* EventObject.eventTarget{object}
* EventObject.eventName{const}

