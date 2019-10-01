#!/usr/bin/env python
# -*- coding: utf-8 -*-
import sys

class Graph(object):
    # init the graph
    def __init__(self, directed=False):
        self._graph_dict = {}
        self._directed = directed

    # return list of vertices
    def get_vertices(self):
        return list(self._graph_dict.keys())

    # add vertice from graph
    def add_vertice(self, vertice):
        if vertice not in self._graph_dict:
            self._graph_dict[vertice] = []

    # remove vertice from graph
    def remove_vertice(self, vertice):
        if vertice in self._graph_dict:
            # remove key (vertice) from dictionary
            self._graph_dict.pop(vertice, None)
            # remove vertice from list of adjacents
            for key in self._graph_dict:
                for v in self._graph_dict[key]:
                    if v == vertice:
                        self._graph_dict[key].remove(vertice)
        else:
            print("Vértice não existe!")


    # get vertice degree
    def vertice_degree(self, vertice):
        if vertice in self._graph_dict:
            adj_vertices =  self.get_adj_vertices(vertice)
            degree = len(adj_vertices) + adj_vertices.count(vertice)
            return degree
        else:
            print("Vértice não existe!")

    # return list of edges
    def get_edges(self):
        edges = []
        for vertice in self._graph_dict:
            for adjacent in self._graph_dict[vertice]:
                if {vertice, adjacent} not in edges:
                    edges.append([vertice, adjacent])
        return edges

    # add edge from graph
    def add_edge(self, u, v):
        if u in self._graph_dict:
            if v not in self._graph_dict[u]:
                self._graph_dict[u].append(v)
                if self._directed == False and u not in self._graph_dict[v]:                    
                    self._graph_dict[v].append(u)
        else:
            self._graph_dict[u] = [v]
            if self._directed == False:
                self._graph_dict[v] = [u]

    # remove edge from graph
    def remove_edge(self, u, v):    
        if u in self._graph_dict:
            self._graph_dict[u].remove(v)

    def get_adj_vertices(self, vertice):
        return self._graph_dict[vertice]
        
    # exist edge between two vertices (u and v)
    def exist_edge(self, u, v):
        return v in self._graph_dict[u] if len(self._graph_dict) > u else -1

    # minimum degree
    def min_degree(self):
        min = 100000000
        for vertice in self._graph_dict:
            vertice_degree = self.vertice_degree(vertice)
            if vertice_degree < min:
                min = vertice_degree
        return min
    
    # maximum degree    
    def max_degree(self):
        max = 0
        for vertice in self._graph_dict:
            vertice_degree = self.vertice_degree(vertice)
            if vertice_degree > max:
                max = vertice_degree
        return max

    def medium_degree(self):
        degrees = 0         
        for vertice in self._graph_dict:
            degrees += self.vertice_degree(vertice)
        return float(degrees) / float(len(self._graph_dict.keys()))

    def is_connected(self, vertices_encountered = None, start_vertice = None):
        if vertices_encountered is None:
            vertices_encountered = set()
        graph_dict = self._graph_dict        
        vertices = list(graph_dict.keys())
        if not start_vertice:
            # chosse a vertice from graph as a starting point
            start_vertice = vertices[0]
        vertices_encountered.add(start_vertice)
        if len(vertices_encountered) != len(vertices):
            for vertice in graph_dict[start_vertice]:
                if vertice not in vertices_encountered:
                    if self.is_connected(vertices_encountered, vertice):
                        return True
        else:
            return True
        return False

    def is_eulerian(self): 
        # Check if all non-zero degree vertices are connected 
        if self.is_connected() == False: 
            return False
        else: 
            #Count vertices with odd degree 
            odd = 0
            for vertice in self._graph_dict:                
                if self.vertice_degree(vertice) % 2 !=0: 
                    odd +=1
  
            if odd == 0 or odd == 2: 
                return True
            elif odd > 2: 
                return False

    def __str__(self):
        return "{}\n({})".format(self.__class__.__name__, dict(self._graph_dict))


if __name__ == "__main__":

    file = open("in.txt", "r")

    directed = True if (int(file.next()) == 1) else False

    graph = Graph(directed)

    number_edges = file.next()

    # c = cost
    for index in range(int(number_edges)):
        u, v, c = file.next().split()
        graph.add_vertice(int(u))
        graph.add_vertice(int(v))
        graph.add_edge(int(u), int(v))

    file.close()

    print("Funções:")
    print("0  - Sair")
    print("1  - Adicionar um vértice")
    print("2  - Remover um vértice")
    print("3  - Listar todos os vértices")
    print("4  - Listar os adjacentes de um vértice")
    print("5  - Obter o grau de um vértice")
    print("6  - Adicionar uma aresta")
    print("7  - Remover uma aresta")
    print("8  - Listar todas as arestas")
    print("9  - Verificar existência de uma aresta")
    print("10 - Obter o grau médio, grau mínimo e grau máximo")
    print("11 - Verificar se o grafo é conexo")
    print("12 - Verificar se o grafo tem um Caminho de Euler")
    print("13 - Exibir grafo")

    while True:
        key = int(input("\nDigite uma função: "))

        if key == 0:
            break

        elif key == 1:
            v = input("Digite um número para identificar o vértice: ")
            graph.add_vertice(int(v))

        elif key == 2:
            v = input("Digite o número identificador do vértice a ser removido: ")
            graph.remove_vertice(int(v))

        elif key == 3:
            print(graph.get_vertices())

        elif key == 4:
            v = input("Digite o número identificador do vértice que deseja listar os seus adjacentes: ")
            print(graph.get_adj_vertices(v))

        elif key == 5:
            v = input("Digite o número identificador do vértice que deseja exibir o grau: ")
            print(graph.vertice_degree(v))

        elif key == 6:
            u, v = raw_input("Digite os dois vértices da aresta (ex: 2 4): ").split()
            graph.add_edge(int(u), int(v))

        elif key == 7:
            u, v = raw_input("Digite os dois vértices da aresta (ex: 2 4) que deseja remover: ").split()
            graph.remove_edge(int(u), int(v))

        elif key == 8:
            print(graph.get_edges())

        elif key == 9:
            u, v = raw_input("Digite os dois vértices da aresta (ex: 2 4) que deseja verificar a existência: ").split()
            answer = graph.exist_edge(int(u), int(v))
            print("Sim" if answer else "Não")

        elif key == 10:
            print("Grau médio = {}").format(round(graph.medium_degree(), 2))
            print("Grau mínimo = {}").format(graph.min_degree())
            print("Grau máximo = {}").format(graph.max_degree())

        elif key == 11:
            answer = graph.is_connected()
            print("Sim" if answer else "Não")

        elif key == 12:
            answer = graph.is_eulerian()
            print("Sim" if answer else "Não")
        elif key == 13:
            print(graph)

        else:
            pass
