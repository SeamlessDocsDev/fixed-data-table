Fixed Data Tables for React
====================================
This is a fork repo for Seamlessdocs.

To release changes to the main app:

1. Bump the version to `$VERSION` in `./package.json`
2. Build: `npm run build`
3. Submit a revision with `arc`
4. Land revision after it gets approved by 2 FE engineers (large change) or 1 (small change)
5. Create version tag: `git tag v$VERSION`
6. Push the new tag: `git push --tags`
7. In the main app, point the dependency on this project to your tag (the part after the `#` in the git URI)

To test changes in the main app:

1. Run `npm run build`
2. Commit everything including the build files
3. Push your branch to GitHub
4. In the main app, point the dependency on this project to your branch (the part after the `#` in the git URI)
5. `npm install` in the main app

====================================

FixedDataTable is a React component for building and presenting data in a flexible, powerful way. It supports standard table features, like headers, columns, rows, header groupings, and both fixed-position and scrolling columns.

The table was designed to handle thousands of rows of data without sacrificing performance. Scrolling smoothly is a first-class goal of FixedDataTable and it's architected in a way to allow for flexibility and extensibility.

Features of FixedDataTable:
* Fixed headers and footer
* Both fixed and scrollable columns
* Handling huge amounts of data
* Variable row heights (with adaptive scroll positions)
* Column resizing
* Performant scrolling
* Customizable styling
* Jumping to a row or column
* Controlled scroll API allows touch support

Things the FixedDataTable **doesn't** do:
* FixedDataTable does not provide a layout reflow mechanism or calculate content layout information such as width and height of the cell contents. The developer has to provide the layout information to the table instead.
* FixedDataTable does not handle sorting of data. Instead it allows the developer to supply data getters that can be sort-, filter-, or tail-loading-aware.
* FixedDataTable does not fetch the data (see above)

### Basic Example

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import {Table, Column, Cell} from 'fixed-data-table';

// Table data as a list of array.
const rows = [
  ['a1', 'b1', 'c1'],
  ['a2', 'b2', 'c2'],
  ['a3', 'b3', 'c3'],
  // .... and more
];

// Render your table
ReactDOM.render(
  <Table
    rowHeight={50}
    rowsCount={rows.length}
    width={5000}
    height={5000}
    headerHeight={50}>
    <Column
      header={<Cell>Col 1</Cell>}
      cell={<Cell>Column 1 static content</Cell>}
      width={2000}
    />
    <Column
      header={<Cell>Col 2</Cell>}
      cell={<MyCustomCell mySpecialProp="column2" />}
      width={1000}
    />
    <Column
      header={<Cell>Col 3</Cell>}
      cell={({rowIndex, ...props}) => (
        <Cell {...props}>
          Data for column 3: {rows[rowIndex][2]}
        </Cell>
      )}
      width={2000}
    />
  </Table>,
  document.getElementById('example')
);
```

Contributions
------------

Use [GitHub issues](https://github.com/facebook/fixed-data-table/issues) for requests.


License
-------

`FixedDataTable` is [BSD-licensed](https://github.com/facebook/fixed-data-table/blob/master/LICENSE). We also provide an additional [patent grant](https://github.com/facebook/fixed-data-table/blob/master/PATENTS).
