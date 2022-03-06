# **REACT Table**
- REACT **Memoizzation** provides us a way to cache the data if the data didnt change, for eg: if on every single render the data didnt change from the previous render, REACT wont have to worry about re-rendering again, can skip some process and save time
1. Get the data we want to display
2. Define the columns for the table
3. Use the data and columns to create a table instance using react-table
4. Define a basic table structure using plan HTML
5. Use table instance created in step 3 to bring life to HTML defined in step 4
6. Included the CSS & styling
- Not columns have to be included in the UI, we can customize the columns to be displayed
```javascript
const { getTableProps, getTableBodyProps, headerGroups, rows, prepareRow } = tableInstance

// getTableProps => required for TABLE HEAD
// getTableBodyProps => required for TABLE BODY
// headerGroups => group of headers
```

```html
return (
        <table className="table table-striped" {...getTableProps()}>
            <thead>
                {
                    headerGroups.map((headerGroup) => (
                        <tr {...headerGroup.getHeaderGroupProps()}>
                            {
                                headerGroup.headers.map((column) => (
                                    <th scope="col" {...column.getHeaderProps()}> {column.render('Header')} </th>
                                ))
                            }
                        </tr>
                    ))
                }
            </thead>
            <tbody {...getTableBodyProps()}>
                {
                    rows.map((row) => {
                        prepareRow(row)
                        return (
                            <tr {...row.getRowProps()}>
                                {
                                    row.cells.map((cell) => {
                                        return <td {...cell.getCellProps()}> {cell.render('Cell')} </td>
                                    })
                                }
                            </tr>
                        )
                    })
                }
            </tbody>
        </table>
    )
```
```javascript
headerGroup.headers.map((column)
<th scope="col" {...column.getHeaderProps()}> {column.render('Header')} </th>
// access the header properties of each element in the Header Groups
// for every header we access each column
// then for each column we render the "Header" property

row.cells.map((cell) => {return <td {...cell.getCellProps()}> {cell.render('Cell')} </td>
// for each row we access the cells
// with each cell we access the cells and call the render function passing in the string cell
// match each cell value according to the column specified
```