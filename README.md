# How to change row background color of Flutter DataTable

The Flutter DataTable widget provides support to change the color of the individual rows based on the requirements.

The following example demonstrates how to change alternate row background color in Flutter DataTable,

## STEP 1
Create data source class extends with DataGridSource for mapping data to the SfDataGrid. 
Override the buildRow method and return the DataGridRowAdapter. You can use the DataGridRowAdapter.color property to change the color of the row.
```xml
class EmployeeDataSource extends DataGridSource {
  EmployeeDataSource({required List<Employee> employees}) {
    _employees = employees;
    updateDataGridRows();
  }

  List<DataGridRow> dataGridRow = [];
  late List<Employee> _employees;

  void updateDataGridRows() {
    dataGridRow = _employees
        .map<DataGridRow>((e) => DataGridRow(cells: [
              DataGridCell<int>(columnName: 'id', value: e.id),
              DataGridCell<String>(columnName: 'name', value: e.name),
              DataGridCell<String>(
                  columnName: 'designation', value: e.designation),
              DataGridCell<int>(columnName: 'salary', value: e.salary),
            ]))
        .toList();
  }

  @override
  List<DataGridRow> get rows => dataGridRow;

  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    Color getBackgroundColor() {
      int index = dataGridRow.indexOf(row) + 1;
      if (index % 2 == 0) {
        return Colors.amber[100]!;
      } else {
        return Colors.red[100]!;
      }
    }

    return DataGridRowAdapter(
        color: getBackgroundColor(),
        cells: row.getCells().map<Widget>((e) {
          return Container(
            alignment: Alignment.center,
            padding: EdgeInsets.all(8.0),
            child: Text(e.value.toString()),
          );
        }).toList());
  }
}
```

## STEP 2
Initialize the SfDataGrid with all the required properties.

```xml
    @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: SfDataGrid(
        source: employeeDataSource,
        columnWidthMode: ColumnWidthMode.fill,
        columns: <GridColumn>[
          GridTextColumn(
              columnName: 'id',
              label: Container(
                  padding: EdgeInsets.all(16.0),
                  alignment: Alignment.center,
                  child: Text(
                    'ID',
                  ))),
          GridTextColumn(
              columnName: 'name',
              label: Container(
                  padding: EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: Text('Name'))),
          GridTextColumn(
              columnName: 'designation',
              label: Container(
                  padding: EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: Text(
                    'Designation',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridTextColumn(
              columnName: 'salary',
              label: Container(
                  padding: EdgeInsets.all(8.0),
                  alignment: Alignment.center,
                  child: Text('Salary'))),
        ],
      ),
    );
  } 
```

<img alt="rowbackground color"  src="https://www.syncfusion.com/uploads/user/kb/flut/flut-4292/flut-4292_img1.jpeg" width="300" height="400" />|