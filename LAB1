#LAB 1
#STUDENT: VALERIA MUÑOZ VILLACRESES

import sys
import numpy as np
from matplotlib import pyplot as pl
import pandas as pd
from datetime import datetime
from matplotlib.colors import LogNorm
import cartopy.crs as ccrs
import cartopy.feature as cfeat
from matplotlib.widgets import Slider

##**Task 1:** The exponential function $e^x$ can also be expressed as
#the series \begin{equation} e^x = 1 + \frac{x}{1!} + \frac{x^2}{2!}
#+ \frac{x^3}{3!} +... \end{equation} However, computers store
#numbers with a finite significand, i.e., $1+\epsilon=1$ if
#$\epsilon<10^{-16}$. How would you write an exponential function using
#recursion based on the above mentioned series while respecting the
#finite significand?
#Task2**Task 2:** How would you solve the previous task using loops?





##**Task 3:** Run the Koch curve recursion and visualize the curve
#for different initial conditions and recursion depths (order) using
#matplotlib.



def koch(x0, y0, rho, phi, order):
    global xtrace, ytrace

    x1, y1 = x0 + rho * np.cos(phi), y0 + rho * np.sin(phi)
    if order:
        x, y = x0, y0
        for angle in [0, np.pi/3, 5*np.pi/3, 0]:
            x, y = koch(x, y, rho / 3.0, phi + angle, order - 1)
    else:
        xtrace.append(x1)
        ytrace.append(y1)

    return (x1, y1)

# this is how one could use that function
xtrace = []
ytrace = []
koch(0, 0, 1, 0, 4)

pl.plot(xtrace, ytrace)
pl.savefig('simple.png')
pl.show()



#Task 4.**Task 4:** First make the same map using the Mercator projection,
#and then have the same script with a for loop iterating over all
#days saving for each day a map as a PNG file. Use a common `norm =
#LogNorm(1, vmax)` with a suitable `vmax` for all frames. In order to
#have a clean canvas in the next iteration of the loop, you have to
#properly close the figure after saving. Save and close the figure
#inside the loop as follows if `i` is your for loop index:

#task 5. *Task 5:** Play around with the above slider widget example and apply
#it to the previous confirmed COVID19 cases example for an interactive
#tool with a slider for time. Then, make this a three panel figure with
#one time slider, but three panels. One for each, confirmed, recovered,
#and death cases.

##CONFIRMED CASES 

#pf = '../../COVID-19/csse_covid_19_data/csse_covid_19_time_series/'
#fn = pf + 'time_series_19-covid-Confirmed.csv'

fn = 'time_series_covid19_confirmed_global.csv'

df = pd.read_csv(fn)
dn = list(df.columns)
da = df.to_numpy()
da = da[:, 2:].astype('float')
lat = da[:, 0]
lon = da[:, 1]
da = da[:, 2:]
da[np.isnan(da)] = 0
dn = dn[4:]

proj = ccrs.Mercator(min_latitude = -70, max_latitude = 70)
dcrs = ccrs.PlateCarree()
cmap = pl.cm.magma_r
norm = LogNorm(1, da.max())

for i in range(da.shape[1]):
    var = da[:, i]
    dat = dn[i].split('/')
    dat = datetime(2000+int(dat[2]), int(dat[0]), int(dat[1]))
    sel = var > 0
    var = var[sel]

    fg = pl.figure(1, (19.2, 10.8))
    fg.suptitle(dat.strftime('%Y-%m-%d'))
    ax = pl.axes(projection = proj)
    ax.set_global()
    ax.gridlines(color = 'white', alpha = 0.5)
    ax.add_feature(cfeat.LAND)
    ax.add_feature(cfeat.OCEAN)
    ax.add_feature(cfeat.COASTLINE)
    ax.add_feature(cfeat.BORDERS, edgecolor = 'gray')
    ob = ax.scatter(lon[sel], lat[sel],
            s = 10 * np.log10(var), c = var,
            cmap = cmap, norm = norm,
            transform = dcrs,
            )
    cb = fg.colorbar(ob, ax = ax,
            aspect = 30, shrink = 0.80,
            )
    cb.set_label('Confirmed cases')
    pl.tight_layout()
    pl.savefig('%04d.png' % (i+1))
    pl.close('all')

def update(val):
    global pc

    pc.remove()
    pc = ax.scatter(x, y, s = s * val, c = s)
    fg.suptitle('scale factor = %i' % int(val))
    fg.canvas.draw_idle()

n = 70
x = np.random.random(n)
y = np.random.random(n)
s = np.random.randint(1, 100, n)

fg = pl.figure()
fg.suptitle('scale factor = 1')
ax = fg.add_axes([0.1, 0.2, 0.8, 0.7])
pc = ax.scatter(x, y, s = s, c = s)

scalax = fg.add_axes([0.1, 0.1, 0.8, 0.01])
slider = Slider(scalax, 'Scale', 0, 50, valinit = 1, valstep = 1)
slider.on_changed(update)
pl.show()

#RECOVERED CASES 


fn = 'time_series_covid19_recovered_global.csv'

df = pd.read_csv(fn)
dn = list(df.columns)
da = df.to_numpy()
da = da[:, 2:].astype('float')
lat = da[:, 0]
lon = da[:, 1]
da = da[:, 2:]
da[np.isnan(da)] = 0
dn = dn[4:]

proj = ccrs.Mercator(min_latitude = -70, max_latitude = 70)
dcrs = ccrs.PlateCarree()
cmap = pl.cm.magma_r
norm = LogNorm(1, da.max())

for i in range(da.shape[1]):
    var = da[:, i]
    dat = dn[i].split('/')
    dat = datetime(2000+int(dat[2]), int(dat[0]), int(dat[1]))
    sel = var > 0
    var = var[sel]

    fg = pl.figure(1, (19.2, 10.8))
    fg.suptitle(dat.strftime('%Y-%m-%d'))
    ax = pl.axes(projection = proj)
    ax.set_global()
    ax.gridlines(color = 'white', alpha = 0.5)
    ax.add_feature(cfeat.LAND)
    ax.add_feature(cfeat.OCEAN)
    ax.add_feature(cfeat.COASTLINE)
    ax.add_feature(cfeat.BORDERS, edgecolor = 'gray')
    ob = ax.scatter(lon[sel], lat[sel],
            s = 10 * np.log10(var), c = var,
            cmap = cmap, norm = norm,
            transform = dcrs,
            )
    cb = fg.colorbar(ob, ax = ax,
            aspect = 30, shrink = 0.80,
            )
    cb.set_label('recovered cases')
    pl.tight_layout()
    pl.savefig('%04d.png' % (i+1))
    pl.close('all')


def update(val):
    global pc

    pc.remove()
    pc = ax.scatter(x, y, s = s * val, c = s)
    fg.suptitle('scale factor = %i' % int(val))
    fg.canvas.draw_idle()

n = 70
x = np.random.random(n)
y = np.random.random(n)
s = np.random.randint(1, 100, n)

fg = pl.figure()
fg.suptitle('scale factor = 1')
ax = fg.add_axes([0.1, 0.2, 0.8, 0.7])
pc = ax.scatter(x, y, s = s, c = s)

scalax = fg.add_axes([0.1, 0.1, 0.8, 0.01])
slider = Slider(scalax, 'Scale', 0, 50, valinit = 1, valstep = 1)
slider.on_changed(update)
pl.show()


#DEAD CASES 

fn = 'time_series_covid19_deaths_global.csv'

df = pd.read_csv(fn)
dn = list(df.columns)
da = df.to_numpy()
da = da[:, 2:].astype('float')
lat = da[:, 0]
lon = da[:, 1]
da = da[:, 2:]
da[np.isnan(da)] = 0
dn = dn[4:]

proj = ccrs.Mercator(min_latitude = -70, max_latitude = 70)
dcrs = ccrs.PlateCarree()
cmap = pl.cm.magma_r
norm = LogNorm(1, da.max())

for i in range(da.shape[1]):
    var = da[:, i]
    dat = dn[i].split('/')
    dat = datetime(2000+int(dat[2]), int(dat[0]), int(dat[1]))
    sel = var > 0
    var = var[sel]

    fg = pl.figure(1, (19.2, 10.8))
    fg.suptitle(dat.strftime('%Y-%m-%d'))
    ax = pl.axes(projection = proj)
    ax.set_global()
    ax.gridlines(color = 'white', alpha = 0.5)
    ax.add_feature(cfeat.LAND)
    ax.add_feature(cfeat.OCEAN)
    ax.add_feature(cfeat.COASTLINE)
    ax.add_feature(cfeat.BORDERS, edgecolor = 'gray')
    ob = ax.scatter(lon[sel], lat[sel],
            s = 10 * np.log10(var), c = var,
            cmap = cmap, norm = norm,
            transform = dcrs,
            )
    cb = fg.colorbar(ob, ax = ax,
            aspect = 30, shrink = 0.80,
            )
    cb.set_label('Dead cases')
    pl.tight_layout()
    pl.savefig('%04d.png' % (i+1))
    pl.close('all')


def update(val):
    global pc

    pc.remove()
    pc = ax.scatter(x, y, s = s * val, c = s)
    fg.suptitle('scale factor = %i' % int(val))
    fg.canvas.draw_idle()

n = 70
x = np.random.random(n)
y = np.random.random(n)
s = np.random.randint(1, 100, n)

fg = pl.figure()
fg.suptitle('scale factor = 1')
ax = fg.add_axes([0.1, 0.2, 0.8, 0.7])
pc = ax.scatter(x, y, s = s, c = s)

scalax = fg.add_axes([0.1, 0.1, 0.8, 0.01])
slider = Slider(scalax, 'Scale', 0, 50, valinit = 1, valstep = 1)
slider.on_changed(update)
pl.show()



    
 
