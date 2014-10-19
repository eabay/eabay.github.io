---
title: Dynamic Grid Panel for Ext JS
date: 2009-01-29 09:00:00
categories:
  - ExtJS
  - Javascript
tags:
  - auto grid
  - CRUD
  - dynamic grid
---

I am using [Ext JS](http://extjs.com) in my web application projects and I decided that it is time to give back to the community.

If you are developing a [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) application and using grids to display data from your database you should define similar column models, fields, readers, stores etc. for your grids. It is not a big concern if it is not the first time you do the same things or you have your own components not to repeat yourself. But what if your database table needs a change in its structure? Let me guess&#8230; You change field and column model definitions in your grids and doing the same again and again even there are small changes.

Here is a small Ext JS component that I wrote:

```javascript
Ext.ux.DynamicGridPanel = Ext.extend(Ext.grid.GridPanel, {
  
  initComponent: function(){
    /**
     * Default configuration options.
     * 
     * You are free to change the values or add/remove options.
     * The important point is to define a data store with JsonReader
     * without configuration and columns with empty array. We are going
     * to setup our reader with the metaData information returned by the server.
     * See http://extjs.com/deploy/dev/docs/?class=Ext.data.JsonReader for more
     * information how to configure your JsonReader with metaData.
     * 
     * A data store with remoteSort = true displays strange behaviours such as
     * not to display arrows when you sort the data and inconsistent ASC, DESC option.
     * Any suggestions are welcome
     */         
    var config = {
      viewConfig: {forceFit: true},
      enableColLock: false,
      loadMask: true,
      border: false,
      stripeRows: true,
      ds: new Ext.data.Store({
        url: this.storeUrl,
        reader: new Ext.data.JsonReader()
      }),
      columns: []
    };
    
    Ext.apply(this, config);
    Ext.apply(this.initialConfig, config);
    
    Ext.ux.DynamicGridPanel.superclass.initComponent.apply(this, arguments);
  },
  
  onRender: function(ct, position){
    this.colModel.defaultSortable = true;
    
    Ext.ux.DynamicGridPanel.superclass.onRender.call(this, ct, position);
    
    /**
     * Grid is not masked for the first data load.
     * We are masking it while store is loading data
     */
    this.el.mask('Loading...');
    this.store.on('load', function(){
      /**
       * Thats the magic! :)
       * 
       * JSON data returned from server has the column definitions
       */
      if(typeof(this.store.reader.jsonData.columns) === 'object') {
	      var columns = [];
	      
	      /**
	       * Adding RowNumberer or setting selection model as CheckboxSelectionModel
	       * We need to add them before other columns to display first	       
	       */	      
	      if(this.rowNumberer) { columns.push(new Ext.grid.RowNumberer()); }
	      if(this.checkboxSelModel) { columns.push(new Ext.grid.CheckboxSelectionModel()); }
        
        Ext.each(this.store.reader.jsonData.columns, function(column){
          columns.push(column);
        });
	      
	      /**
	       * Setting column model configuration
	       */
	      this.getColumnModel().setConfig(columns);
      }
      /**
       * Unmasking grid
       */
      this.el.unmask();
    }, this);
    /**
     * And finally load the data from server!
     */
    this.store.load();
  }
});
```

How to use it?

```javascript
new Ext.ux.DynamicGridPanel({
  id: 'my-grid',
  storeUrl: 'server/url/address/',
  rowNumberer: true,
  checkboxSelModel: true,
  sm: new Ext.grid.CheckboxSelectionModel(),
});
```

And here is the JSON which should be returned from server to dynamically create column and field definitions:

```json
{
    "metaData": {
        "totalProperty": "total",
        "root": "records",
        "id": "id",
        "fields": [
            {
                "name": "id",
                "type": "int" 
            },
            {
                "name": "name",
                "type": "string" 
            } 
        ] 
    },
    "success": true,
    "total": 50,
    "records": [
        {
            "id": "1",
            "name": "AAA" 
        },
        {
            "id": "2",
            "name": "BBB" 
        } 
    ],
    "columns": [
        {
            "header": "#",
            "dataIndex": "id" 
        },
        {
            "header": "User",
            "dataIndex": "name" 
        } 
    ]
}
```

The code itself is somewhat self-explanatory but for newbie users [learning center](http://extjs.com/learn) is a good start to understand how to extend Ext JS or simply understand how the framework works.

Suggestions and comments are welcome...
