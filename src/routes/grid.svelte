<script>
  import { onMount } from "svelte";
  import DUMY from "../dumy/grid_dumy_data.json";
  import DUMY_DATA from "../dumy/tree";
  onMount(() => {
    // https://nhn.github.io/tui.grid/latest/tutorial-example26-infinite-scroll
    const Grid = require("tui-grid"); /* CommonJS */
    // 베이직
    // const instance = new Grid({
    //   el: window.document.getElementById("grid"), // Container element
    //   columns: [
    //     {
    //       header: "Name",
    //       name: "name"
    //     },
    //     {
    //       header: "Artist",
    //       name: "artist"
    //     },
    //     {
    //       header: "Release",
    //       name: "release"
    //     },
    //     {
    //       header: "Genre",
    //       name: "genre"
    //     }
    //   ],
    //   data: DUMY.sample
    // });
    // // instance.resetData(newData); // Call API of instance's public method
    // Grid.applyTheme("striped"); // Call API of static method

    // 커스텀
    class CustomTextEditor {
      constructor(props) {
        const el = document.createElement("input");
        const { maxLength } = props.columnInfo.editor.options;

        el.type = "text";
        el.maxLength = maxLength;
        el.value = String(props.value);

        this.el = el;
      }
      getElement() {
        return this.el;
      }
      getValue() {
        return this.el.value;
      }
      mounted() {
        this.el.select();
      }
    }

    // const grid = new Grid({
    //   el: document.getElementById("grid"),
    //   scrollX: false,
    //   scrollY: false,
    //   columns: [
    //     {
    //       header: "Name",
    //       name: "name",
    //       onBeforeChange(ev) {
    //         console.log("Before change:" + ev);
    //         ev.stop();
    //       },
    //       onAfterChange(ev) {
    //         console.log("After change:" + ev);
    //       },
    //       editor: "text"
    //     },
    //     {
    //       header: "Artist",
    //       name: "artist",
    //       onBeforeChange(ev) {
    //         console.log("Before change:" + ev);
    //       },
    //       onAfterChange(ev) {
    //         console.log("After change:" + ev);
    //       },
    //       editor: {
    //         type: CustomTextEditor,
    //         options: {
    //           maxLength: 10
    //         }
    //       }
    //     },
    //     {
    //       header: "Type",
    //       name: "typeCode",
    //       onBeforeChange(ev) {
    //         console.log("Before change:" + ev);
    //       },
    //       onAfterChange(ev) {
    //         console.log("After change:" + ev);
    //       },
    //       formatter: "listItemText",
    //       editor: {
    //         type: "select",
    //         options: {
    //           listItems: [
    //             { text: "Deluxe", value: "1" },
    //             { text: "EP", value: "2" },
    //             { text: "Single", value: "3" }
    //           ]
    //         }
    //       }
    //     },
    //     {
    //       header: "Genre",
    //       name: "genreCode",
    //       onBeforeChange(ev) {
    //         console.log("Before change:" + ev);
    //       },
    //       onAfterChange(ev) {
    //         console.log("After change:" + ev);
    //       },
    //       formatter: "listItemText",
    //       editor: {
    //         type: "checkbox",
    //         options: {
    //           listItems: [
    //             { text: "Pop", value: "1" },
    //             { text: "Rock", value: "2" },
    //             { text: "R&B", value: "3" },
    //             { text: "Electronic", value: "4" },
    //             { text: "etc.", value: "5" }
    //           ]
    //         }
    //       },
    //       copyOptions: {
    //         useListItemText: true // when this option is used, the copy value is concatenated text
    //       }
    //     },
    //     {
    //       header: "Grade",
    //       name: "grade",
    //       onBeforeChange(ev) {
    //         console.log("Before change:" + ev);
    //       },
    //       onAfterChange(ev) {
    //         console.log("After change:" + ev);
    //       },
    //       copyOptions: {
    //         useListItemText: true
    //       },
    //       formatter: "listItemText",
    //       editor: {
    //         type: "radio",
    //         options: {
    //           listItems: [
    //             { text: "★☆☆", value: "1" },
    //             { text: "★★☆", value: "2" },
    //             { text: "★★★", value: "3" }
    //           ]
    //         }
    //       }
    //     }
    //   ]
    // });
    // grid.resetData(DUMY.customEditor);
    // datasource
    // const grid = new Grid({
    //   el: document.getElementById("grid"),
    //   data: {
    //     api: {
    //       readData: { url: "/api/readData", method: "GET" }
    //     }
    //   },
    //   scrollX: false,
    //   scrollY: false,
    //   minBodyHeight: 30,
    //   rowHeaders: ["rowNum"],
    //   pageOptions: {
    //     perPage: 5
    //   },
    //   columns: [
    //     {
    //       header: "Name",
    //       name: "name"
    //     },
    //     {
    //       header: "Artist",
    //       name: "artist"
    //     },
    //     {
    //       header: "Type",
    //       name: "type"
    //     },
    //     {
    //       header: "Release",
    //       name: "release"
    //     },
    //     {
    //       header: "Genre",
    //       name: "genre"
    //     }
    //   ]
    // });
    // tree 
    const grid = new Grid({
      el: document.getElementById('grid'),
      data: DUMY_DATA,
      rowHeaders: ['checkbox'],
      bodyHeight: 500,
      treeColumnOptions: {
        name: 'name',
        useCascadingCheckbox: true
      },
      columns: [
        {
          header: 'Name',
          name: 'name',
          width: 300
        },
        {
          header: 'Artist',
          name: 'artist'
        },
        {
          header: 'Type',
          name: 'type'
        },
        {
          header: 'Release',
          name: 'release'
        },
        {
          header: 'Genre',
          name: 'genre'
        }
      ]
    });

    grid.on('expand', ev => {
      const { rowKey } = ev;
      const descendantRows = grid.getDescendantRows(rowKey);

      console.log('rowKey: ' + rowKey);
      console.log('descendantRows: ' + descendantRows);
    });

    grid.on('collapse', ev => {
      const { rowKey } = ev;
      const descendantRows = grid.getDescendantRows(rowKey);

      console.log('rowKey: ' + rowKey);
      console.log('descendantRows: ' + descendantRows);
    });
  });
</script>

<svelte:head>
  <title>Grid</title>
</svelte:head>

<h1>Grid this site</h1>

<p>This is the 'grid' page. There's not much here.</p>
<div id="grid" />


