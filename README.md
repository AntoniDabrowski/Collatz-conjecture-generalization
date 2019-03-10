# Collatz-conjecture-generalization

from matplotlib import pyplot as plt


def div(pair):
 if pair==[0,0]:
    return pair
 if pair[0] % 2 == 0 and pair[1] % 2 == 0:
     pair = div([int(pair[0] / 2), int(pair[1] / 2)])
 return pair

def check(a, b):
 set_A = set()
 if a == 0 and b == 1: return 1
 if a % 2 != b % 2: return 0
 for c in range(1, 100):
     too_much = 1
     set_B = set()
     while c != 1 and c not in set_A:
         if too_much > 50000 or c in set_B:
             return 0
         set_B.add(c)
         c = step(c, a, b)
         too_much += 1
     set_A.update(set_B)
 return 1

def step(c, a, b):
 return c / 2 if c % 2 == 0 else a * c + b


if __name__ == "__main__":
 size = 17
 x_first = [0]
 x_next = []
 y_first = [0]
 y_next = []
 for x_ in range(size):
    for y_ in range(size):
       if x_%2==y_%2==0:
          if check(div([y_-int(size/2),x_-int(size/2)])[0],div([y_-int(size/2),x_-int(size/2)])[1]):
             y_first.append(x_-int(size/2))
             x_first.append(y_-int(size/2))
       else:
          if check(div([y_-int(size/2),x_-int(size/2)])[0],div([y_,x_-int(size/2)])[1]):
             y_next.append(x_-int(size/2))
             x_next.append(y_-int(size/2))


 fig, ax = plt.subplots()
 ax.scatter(x_first, y_first, label='Copies', color='blue')
 ax.scatter(x_next, y_next, label='First time', color='red')
 legend = ax.legend(loc='bottom right', fontsize='x-large')
 plt.xlabel('a size')
 plt.ylabel('b size')
 plt.title('Collatz conjecture generalization')
 plt.show()
