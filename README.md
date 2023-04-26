#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Obra
{
private:
  string nombre;
  string fecha;
public:
  Obra (string nombre, string fecha)
  {
    cout << "Se ha creado la obra " << nombre << " en la fecha de " << fecha << endl;
    this->nombre = nombre;
    this->fecha = fecha;
  }
  ~Obra ()
  {
    cout << "Se ha eliminado la obra " << this->nombre << endl;
  }
};

class Artista
{
public:
  string nombre;
  int edad;
  vector < Obra * > obrasContainer;
public:
  void agregarObra (Obra * _obra)
  {
    this->obrasContainer.push_back (_obra);
  }
  void crearObra ()
  {
    string nombre, fecha;
    cout << "Elija el nombre de la obra: ";
    cin >> nombre;
    cout << "Elija la fecha: ";
    cin >> fecha;
    agregarObra (new Obra (nombre, fecha));
  }
  Artista (string nombre, int edad)
  {
    cout << "Se ha creado el artista " << nombre << " de edad "<< edad <<  endl;
    this->nombre = nombre;
    this->edad = edad;
  }
  ~Artista ()
  {
    cout << "Se ha eliminado el artista " << this->nombre << endl;
    for (int i = 0; i < this->obrasContainer.size (); i++)
      {
        delete this->obrasContainer[i];
      }
  }
};

int main ()
{
  vector < Artista * > artistas;
  int opcion;
  do
    {
      cout << " MENU DE OPCIONES " << endl;
      cout << "1. Agregar artista" << endl;
      cout << "2. Crear obra" << endl;
      cout << "3. Salir" << endl;
      cout << "Elija una opcion: ";
      cin >> opcion;
      switch (opcion)
  {
  case 1:
    {
      string nombre;
      int edad;
      cout << "Ingrese el nombre del artista: ";
      cin >> nombre;
      cout << "Ingrese la edad del artista: ";
      cin >> edad;
      artistas.push_back (new Artista (nombre, edad));
      break;
    }
  case 2:
    {
      int artistaIndex;
      cout << "Seleccione el artista que va a crear la obra:" << endl;
      for (int i = 0; i < artistas.size (); i++)
        {
          cout << i + 1 << ". " << artistas[i]->nombre << endl;
        }
      cout << "Elija una opcion: ";
      cin >> artistaIndex;
      artistas[artistaIndex - 1]->crearObra ();
      break;
    }
  case 3:
    {
      cout << "Fin del Programa" << endl;
      break;
    }
  default:
    {
      cout << "Opcion invalida. Intente de nuevo." << endl;
      break;
    }
  }
    }
  while (opcion != 3);

  // Liberar memoria
  for (int i = 0; i < artistas.size (); i++)
    {
      delete artistas[i];
    }

  return 0;
}
