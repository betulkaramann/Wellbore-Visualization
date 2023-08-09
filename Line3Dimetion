import pandas as pd
import plotly.graph_objects as go
import numpy as np


def cartesian_to_spherical(x_positions, y_positions, z_values):
    r_values = np.sqrt(x_positions**2 + y_positions**2 + z_values**2)
    theta_values = np.arctan2(y_positions, x_positions)
    
    theta_values = np.deg2rad(theta_values)
    
    phi_values = np.where(
        np.isclose(r_values, 0) | np.isclose(r_values, 0.0),
        np.where(np.isclose(z_values, 0), 0.0, np.pi),
        np.arccos(z_values / r_values)
    )
    
    return r_values, theta_values, phi_values

excel_file_path = 'WellboreGeometrisi.xls' 
df = pd.read_excel(excel_file_path)

numeric_columns = ['North[m]', 'East[m]', 'TVD[m]', 'Azi[deg]', 'MD[m]']
df[numeric_columns] = df[numeric_columns].replace({'[N]': '', '[E]': '', '[S]': '', '[W]': '', ',': '.'}, regex=True).astype(float)

x_positions = df['North[m]'].values
y_positions = df['East[m]'].values
z_values = df['TVD[m]'].values

r_values, theta_values, phi_values = cartesian_to_spherical(x_positions, y_positions, z_values)
df['r'] = r_values
df['theta'] = theta_values
df['phi'] = phi_values

fig = go.Figure(data=go.Streamtube(
    x=x_positions,
    y=y_positions,
    z=z_values,
    u=r_values,
    v=theta_values,
    w=phi_values,
    sizeref = 0.3,
    colorscale = 'Portland',
    showscale = False,
    maxdisplayed = 3000

    )
)
fig.update_layout(
    title='3D Streamtube Wellbore Visualization',
    scene=dict(
        xaxis_title='North [m]',
        yaxis_title='East [m]',
        zaxis_title='TVD [m]',
        aspectratio=dict(x=1, y=1, z=0.7),
        aspectmode='manual',
        camera=dict(up=dict(x=0, y=0, z=1), eye=dict(x=0, y=1.0707, z=1))
    ),
    width=800,
    height=700,
    autosize=False,
    margin=dict(t=20, b=20, l=20, r=20)
)

fig.show()
