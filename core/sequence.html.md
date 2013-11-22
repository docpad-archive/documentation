```
title: "Sequence Flows"
```


## Legend

```
: Object/Area
> method
< procedure
>> background method
<< background procedure
? condition
```


## Run Action

```
: Interface
	> command
		: Core
			> run
				> server
				> generate
					> createProgress
					> createRengerateTimer
					> generatePrepare

						? if reset is true
							? if source directory doesn't exist
								< error
							> resetCollections
								< reset database
							> populateCollections
								> parseDirectory documentsPath
								> parseDirectory filesPath
								> parseDirectory layoutsPaths
								> emitSerial "populateCollectionsBefore"
									: Tumblr Plugin
										> fetchTumblrData
											< json data from tumblr api
										< add each tumblr post into docpad database
							< use all models

						? if reset is false
							< use changed models

						> emitSerial "generateAfter"

					> generateLoad
						> loadFiles opts.collection
						< add references and layout children to opts.collection

					> generateRender
						> contextualizeFiles
							> emitSerial "contextualizeBefore"
							> file.contextualize
								< meta data normalized
								< layout determined
							> emitSerial "conextualizeAfter"

						> renderFiles
							> emitSerial "renderBefore"
							> renderCollection(referencesOthers:false)
							+ renderCollection(referencesOthers:true) < for each render pass
								> file.render
									> emitSerial "render"
									> emitSerial "renderDocument"
							> emitSerial "renderAfter"
						> writeFiles

					> generatePostpare
						> emitSerial "generateAfter"


				> watch
					>> watchr.watch config.reloadPaths
						>> docpad.load
							>> docpad.generate reset:true
					>> watchr.watch config.regeneratePAths
						>> docpad.generate reset:true
					>> watchr.watch config.srcPath
						>> docpad.generate
```

