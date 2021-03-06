[![Build Status](https://travis-ci.org/KevinFasusi/supplychainpy.svg?branch=master)](https://travis-ci.org/KevinFasusi/supplychainpy?branch=master)
[![Documentation Status](https://readthedocs.org/projects/supplychainpy/badge/?version=latest)](http://supplychainpy.readthedocs.org/en/latest/?badge=latest)
[![Coverage Status](https://coveralls.io/repos/github/KevinFasusi/supplychainpy/badge.svg?branch=master)](https://coveralls.io/github/KevinFasusi/supplychainpy?branch=master)
[![PyPI version](https://badge.fury.io/py/supplychainpy.svg)](https://badge.fury.io/py/supplychainpy)

#Supplychainpy

Supplychainpy is a Python library for supply chain analysis, modeling and simulation. Use in conjunction with popular
data analysis libraries and excel tools such as xlwings or openpyxl (for Excel spreadsheet applications).

The library is currently in early stages of development, so not ready for use in production. However some fun can be had
by passing a csv or text file in the correct format. For quick exploration, the `analyse_orders_abcxyz_from_file`
will output the following inventory analysis:
- economic order quantities
- safety stock
- abc xyz classification
- demand variability
- ...

##Quick Install

The easiest way to install supplychainpy is via pip: `pip install supplychainpy`.

An alternative is to clone the repository and run `python setup.py install`

##Dependencies

- NumPy

##Optional Dependencies

- pandas
- matplotlib
- xlwings
- openpyxl


##Python Version

- python 3.5

##Quick Guide
1. Fire up the python interpreter or `ipython notebook` from the command line.

2. Format the `.csv` or `.txt`.e.g `sku id`, `order1`, `order2`,... `orders12`, `unit cost`, `lead time`,

At the moment the lead-time must match the orders time bucket i.e both should be in days, weeks or months. This will
change promptly.

```python
	from xlwings import Workbook, Range
    from supplychainpy.model_inventory import analyse_orders_abcxyz_from_file
    wb = Workbook(r'~/Desktop/test.xlsx'), Range
    abc = analyse_orders_abcxyz_from_file(file_path="data.csv", z_value= 1.28, reorder_cost=5000, file_type="csv")

	for index ,sku in enumerate(abc.orders, 1):
        Range('A'+ str(index)).value = sku.sku_id
        Range('B' + str(index)).value = float(sku.economic_order_qty)
        Range('C' + str(index)).value = float(sku.revenue)
        Range('D' + str(index)).value = sku.abcxyz_classification

```

or get the whole analysis using:

```python
	from supplychainpy.model_inventory import analyse_orders_abcxyz_from_file
    abc = analyse_orders_abcxyz_from_file(file_path="data.csv", z_value=Decimal(1.28),
                                     reorder_cost=Decimal(5000), file_type="csv")
	for sku in abc.orders:
	    print(sku.orders_summary())
```

Further examples and explanations will be available in the documentation. Please find below.

Documentation: [supplychainpy.readthdocs](http://supplychainpy.readthedocs.org/)

Website: [supplychainpy.org](http://www.supplychainpy.org/)

Forum: [google groups](https://groups.google.com/forum/#!forum/supplychainpy)





