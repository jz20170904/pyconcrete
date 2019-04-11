# pyconcrete
python module for drawing concrete plan details.

it aims to draw such a beam and columns at the end.

![image](https://user-images.githubusercontent.com/8196112/55085621-97acb100-50c4-11e9-91e6-7afcf2d7dbbc.png)

![image](https://user-images.githubusercontent.com/8196112/55085845-f70ac100-50c4-11e9-98c4-05240751b4d5.png)


It includes BeamType class that itself includes number of Beams class.
at present it can draw beamtype shape, beamsize text, dimension lines and axes lines.

## Dependencies
- python >= 3.7
- ezdxf

## Usage

This example show how you can create BeamType and then export that to dxf file
with ezdxf python package for example.

```python
import pytest

import ezdxf

from pyconcrete.beamtype import beamtype, beamtypedxf


bt1 = beamtype.BeamType(spans_len=[204, 420, 350],
                        beams_dimension=[(40, 45), (40, 45), (40, 45)],
                        columns_width=dict(
    bot=[0, 45, 40, 50],
    top=[0, 45, 40, 45],),
    stirrups_len=[None, [85, 85], [85, 85]],
    axes_name=[('C', 1), ('D', 1), ('E', 1), ('F', 1)],)


bt2 = beamtype.BeamType(spans_len=[204, 420, 350],
                        beams_dimension=[(40, 60), (30, 60), (50, 60)],
                        columns_width=dict(
    bot=[45, 45, 40, 50],
    top=[40, 45, 40, 45],),
    stirrups_len=[None, [115, 115], [85, 85]],
    axes_name=[('A', 1), ('B', 1), ('C', 1), ('D', 1)],)


bt3 = beamtype.BeamType(spans_len=[204, 420, 350],
                        beams_dimension=[(40, 40), (30, 40), (50, 40)],
                        columns_width=dict(
    bot=[45, 45, 40, 50],
    top=[0, 0, 0, 0],),
    stirrups_len=[None, [115, 115], [85, 85]],
    axes_name=[('A', 1), ('B', 1), ('C', 1), ('D', 1)],)


bt4 = beamtype.BeamType(spans_len=[204, 420, 350],
                        beams_dimension=[(40, 40), (30, 40), (50, 40)],
                        columns_width=dict(
    bot=[0, 0, 0, 0],
    top=[45, 45, 40, 50],),
    stirrups_len=[None, [115, 115], [85, 85]],
    axes_name=[('A', 1), ('B', 1), ('C', 1), ('D', 1)],)

new_dwg = ezdxf.new('AC1024', setup=True)
msp = new_dwg.modelspace()
for i, bt in enumerate((bt1, bt2, bt3, bt4)):
    btdxf = beamtypedxf.BeamTypeDxf(bt, new_dwg)
    btdxf.to_dxf()
    msp.add_blockref(bt.uid, (200, i * 150))
new_dwg.saveas('/home/ebi/beamtype1.dxf')

# scaled beamtype
new_dwg = ezdxf.new('AC1024', setup=True)
msp = new_dwg.modelspace()
h = 100
v = 25
for i, bt in enumerate((bt1, bt2, bt3, bt4)):
    bt.scale = (h, v)
    btdxf = beamtypedxf.BeamTypeDxf(bt, new_dwg)
    btdxf.to_dxf()
    msp.add_blockref(bt.uid, (200 / h, i * 130 / v))
new_dwg.saveas('/home/ebi/scaled_beamtype1.dxf')

```


## output

This is output at peresent, but I'll add scale parameter and styles to seems look better!

### None scaled beamtype:
![image](https://user-images.githubusercontent.com/8196112/56002669-81b00a80-5cd8-11e9-96f0-4d732cdd973d.png)

### Scaled beamtype:
![image](https://user-images.githubusercontent.com/8196112/56002521-077f8600-5cd8-11e9-8eac-7ae6331da61a.png)


