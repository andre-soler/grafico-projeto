import pandas as pd
df = pd.read_csv('/content/imigrantes_canada.csv')
df
df.info()
df.set_index('País', inplace=True)
anos = list(map(str, range(1980, 2014)))
anos
brasil = df.loc['Brasil', anos]
brasil
brasil_dict = {'ano': brasil.index.tolist(), 'imigrantes': brasil.values.tolist()}
dados_brasil = pd.DataFrame(brasil_dict)
dados_brasil
import matplotlib.pyplot as plt
plt.figure(figsize=(8,4))
plt.plot(dados_brasil['ano'], dados_brasil['imigrantes'])
plt.title('Imigração do rasil para o Canadá')
plt.xlabel('Ano')
plt.ylabel('Número de Imigantes')
plt.xticks(['1980', '1985', '1990', '1995', '2000', '2005', '2010'])
plt.show()
fig, ax = plt.subplots(figsize=(8,4))
ax.plot(dados_brasil['ano'], dados_brasil['imigrantes'], lw=3, color='g')
ax.set_title('Imigração do Brasil para o Canadá\n1980 a 2013', fontsize=18, loc='left')
ax.set_xlabel('Ano', fontsize=14)
ax.set_ylabel('Número de Imigrantes', fontsize=14)
ax.xaxis.set_tick_params(labelsize=12)
ax.yaxis.set_tick_params(labelsize=12)
ax.xaxis.set_major_locator(plt.MultipleLocator(5))
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)
fig.savefig('imigracao_brasil_canada.png', transparent=False, dpi=300, bbox_inches='tight')
plt.show()
df.head()
america_sul = df.query('Região =="América do Sul"')
america_sul
cores = []
for pais in america_sul_sorted.index:
  if pais == 'Brasil':
    cores.append('green')
  else:
     cores.append('gray')


fig, ax = plt.subplots(figsize=(12,5))
ax.barh(america_sul_sorted.index, america_sul_sorted['Total'], color=cores)
ax.set_title('Imigração da América: Brasil foi o quarto país com mais imigrantes\npara o Canadá no período de 1980 a 2013', loc='left', fontsize=18)
ax.set_xlabel('Número de Imigrantes', fontsize=14)
ax.set_ylabel('')
ax.xaxis.set_tick_params(labelsize=12)
ax.yaxis.set_tick_params(labelsize=12)

for i, v in enumerate(america_sul_sorted['Total']):
  ax.text(v + 20, i, str(v), color='black', fontsize=10, ha='left', va='center')
  ax.set_frame_on(False)
  ax.get_xaxis().set_visible(False)
  ax.tick_params(axis='both', which='both', length=0)

  fig.savefig('imigracao_america_sul.png', transparent=False, dpi=300, bbox_inches='tight')

plt.show()

print(fig.canvas.get_supported_filetypes())
america_sul_sorted = america_sul.sort_values('Total', ascending=True)
import seaborn as sns
sns.set_theme()
top_dez = df.sort_values('Total', ascending=False).head(10)
top_dez
sns.barplot(data=top_dez, x=top_dez.index, y='Total')
