import pandas as pd
import plotly.graph_objects as go

excel_file_path = 'WellboreGeometrisi.xls'
df = pd.read_excel(excel_file_path)

df['MD[m]'] = df['MD[m]'].str.replace(',', '.', regex=True).str.replace('==> ', '', regex=True).astype(float)

depth = df['MD[m]']
x_positions = df['North[m]']
y_positions = df['East[m]']
tvd = df['TVD[m]']

fig = go.Figure(data=[go.Scatter3d(
    x=x_positions,
    y=y_positions,
    z=tvd,
    mode='markers+lines',
    marker=dict(size=4, color=depth, colorscale='Viridis'),
    line=dict(color='darkblue', width=2)
)])

fig.update_layout(
    scene=dict(
        xaxis_title='North [m]',
        yaxis_title='East [m]',
        zaxis_title='TVD [m]',
    ),
    title='3D Wellbore Visualization',
)

fig.show()
