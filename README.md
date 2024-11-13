[![Visitors](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FRoyiAvital%2FStackExchangeCodes&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Visitors+%28Daily+%2F+Total%29&edge_flat=false)](https://github.com/RoyiAvital/Julia100Exercises)

# 100 Ejercicios de Julia con soluciones

Una serie de ejercicios introductorios a Julia. Basado en [100 NumPy Exercises](https://github.com/rougier/numpy-100).


Para generar este archivo:
1. Clone el repositorio (o descargarlo).
 2. Active e instanciar el proyecto.
3. Run:
```Julia
using Literate;
Literate.markdown("Julia100Exercises.jl", name = "README", execute = true, flavor = Literate.CommonMarkFlavor());
```

**Remark**: Tested with Julia `1.8.2`.

**To Do**:
1. Reevaluar el nivel de dificultad de cada pregunta.

````julia
using Literate;
using LinearAlgebra;
using Statistics;
using Dates;
using DelimitedFiles;
using UnicodePlots;
using Random;
using Tullio;
using StaticKernels;
````

## Pregunta 001

Importe el paquete `LinearAlgebra` bajo el nombre` LA`. (★ ☆☆)

````julia
import LinearAlgebra as LA;
````

## Pregunta 002

Print the version of Julia. (★☆☆)

````julia
println(VERSION);
````

````julia
1.8.2
````

## Pregunta 003
Cree un vector no inicializado de tamaño 10 de `Float64`. (★ ☆☆)

````julia
vA = Vector{Float64}(undef, 10)
````

````julia-repl
10-element Vector{Float64}:
 0.0
 1.314224183e-315
 1.314224183e-315
 0.0
 1.314248214e-315
 1.31427351e-315
 0.0
 1.314248214e-315
 1.314106556e-315
 0.0
````

Que es equivalente a

````julia
vA = Array{Float64, 1}(undef, 10)
````

````
10-element Vector{Float64}:
 0.0
 1.314248214e-315
 1.314106556e-315
 0.0
 1.314248214e-315
 1.314106556e-315
 0.0
 1.314248214e-315
 1.314106556e-315
 0.0
````

## Pregunta 004

Encuentre el tamaño de la memoria de cualquier matriz. (★☆☆)

````julia
sizeof(vA)
````

````
80
````

## Pregunta 005

Muestre la documentación del método `+` (add). (★☆☆)

````julia
@doc +
````

```
+(x, y...)
```

Operador de adición. `x+y+z+...` llama a esta función con todos los argumentos, es decir, `+(x, y, z, ...)`.

# Examples

```jldoctest
julia> 1 + 20 + 4
25

julia> +(1, 20, 4)
25
```

```
dt::Date + t::Time -> DateTime
```

La adición de una `Date` con un `Time` produce una `DateTime`. Las partes de la hora, el minuto, la segunda y el milisegundo del 'Tiempo' se usan junto con el año, el mes y el día de la 'Fecha' para crear el nuevo 'DateTime`. Microsegundos o nanosegundos distintos de cero en el tipo `Time` darán como resultado un 'InexactError` lanzado.

## Pregunta 006

Cree un vector de ceros de tamaño 10 pero que el quinto valor sea 1. (★☆☆)

````julia
vA = zeros(10);
vA[5] = 1.0;
vA
````

````
10-element Vector{Float64}:
 0.0
 0.0
 0.0
 0.0
 1.0
 0.0
 0.0
 0.0
 0.0
 0.0
````

## Pregunta 007

Cree un vector con los valores enteros entre 7 y 12. (★ ☆☆)

````julia
vA = 7:12
````

````
7:12
````

The above is efficient type. In order to explicitly create a vector:

````julia
vA = collect(7:12)
````

````
6-element Vector{Int64}:
  7
  8
  9
 10
 11
 12
````

## Pregunta 008

Revertir un vector (el primer elemento se convierte en el último). (★☆☆)

````julia
vA = collect(1:3);
vB = vA[end:-1:1];
vB
````

````
3-element Vector{Int64}:
 3
 2
 1
````

Alternativa 001:

````julia
vB = reverse(vA);
````

Alternativa 002 ("In place"/sin usar memoria adicional):

````julia
reverse!(vA);
vA
````

````
3-element Vector{Int64}:
 3
 2
 1
````

## Pregunta 009

Cree una matriz `3x3` con valores los valores del 0 a 8. (★ ☆☆)

````julia
mA = reshape(0:8, 3, 3)
````

````
3×3 reshape(::UnitRange{Int64}, 3, 3) with eltype Int64:
 0  3  6
 1  4  7
 2  5  8
````

Otra manera es:

````julia
mA = Matrix{Float64}(undef, 3, 3);
mA[:] = 0:8;
````

## Pregunta 010

Encuentre los índices de elementos no cero de `[1, 2, 0, 0, 4, 0]`. (★ ☆☆)

````julia
findall(!iszero, [1, 2, 0, 0, 4, 0])
````

````
3-element Vector{Int64}:
 1
 2
 5
````

## Pregunta 011

Cree una matriz de identidad 3x3. (★ ☆☆)

````julia
mA = I(3)
````

````
3×3 LinearAlgebra.Diagonal{Bool, Vector{Bool}}:
 1  ⋅  ⋅
 ⋅  1  ⋅
 ⋅  ⋅  1
````

Un método alternativo (matriz explícita) sería:

````julia
mA = Matrix(I, 3, 3) #<! For Float64: Matrix{Float64}(I, 3, 3)
````

````
3×3 Matrix{Bool}:
 1  0  0
 0  1  0
 0  0  1
````

## Pregunta 012

Cree una matriz `2x2x2` con valores aleatorios. (★ ☆☆)

````julia
mA = randn(2, 2, 2)
````

````
2×2×2 Array{Float64, 3}:
[:, :, 1] =
 -1.34961   -0.225955
  0.116267   1.03802

[:, :, 2] =
  0.737672  2.2642
 -0.839961  0.218133
````

## Pregunta 013

Cree una matriz `5x5` con valores aleatorios y encuentre los valores mínimos y máximos. (★ ☆☆)

````julia
mA = rand(5, 5);
minVal = minimum(mA)
````

````
0.02305480092860468
````

````julia
maxVal = maximum(mA)
````

````
0.9708814560256962
````

Usando `extrema ()` se podría obtener ambos valores a la vez:

````julia
minVal, maxVal = extrema(mA);
````

## Pregunta 014

Cree un vector aleatorio de tamaño 30 y encuentre el valor promedio. (★ ☆☆)

````julia
meanVal = mean(randn(30))
````

````
-0.04218053798839749
````

## Pregunta 015

Cree una matriz 2D con 1 en el borde y 0 en el interior. (★ ☆☆)

````julia
mA = zeros(4, 4);
mA[:, [begin, end]] .= 1;
mA[[begin, end], :] .= 1;
mA
````

````
4×4 Matrix{Float64}:
 1.0  1.0  1.0  1.0
 1.0  0.0  0.0  1.0
 1.0  0.0  0.0  1.0
 1.0  1.0  1.0  1.0
````

Una forma alternativa (diferentes dimensiones):

````julia
mA = ones(4, 5);
mA[2:(end - 1), 2:(end - 1)] .= 0;
````

Usando una línea de código:

````julia
mA = zeros(4, 5);
mA[[LinearIndices(mA)[cartIdx] for cartIdx in CartesianIndices(mA) if (any(cartIdx.I .== 1) || cartIdx.I[1] == size(mA, 1) || cartIdx.I[2] == size(mA, 2))]] .= 1;
````

por [Tomer Arnon](https://github.com/tomerarnon):

````julia
numRows = 5;
numCols = 4;
mA = Int[ii ∈ (1, numRows) || jj ∈ (1, numCols) for ii in 1:numRows, jj in 1:numCols];
````

## Pregunta 016

Agregue un borde de ceros alrededor de la matriz. (★ ☆☆)

````julia
mB = zeros(size(mA) .+ 2);
mB[2:(end - 1), 2:(end - 1)] = mA;
mB
````

````
7×6 Matrix{Float64}:
 0.0  0.0  0.0  0.0  0.0  0.0
 0.0  1.0  1.0  1.0  1.0  0.0
 0.0  1.0  0.0  0.0  1.0  0.0
 0.0  1.0  0.0  0.0  1.0  0.0
 0.0  1.0  0.0  0.0  1.0  0.0
 0.0  1.0  1.0  1.0  1.0  0.0
 0.0  0.0  0.0  0.0  0.0  0.0
````

## Pregunta 017

Evaluar las siguientes expresiones. (★ ☆☆)

````julia
0 * NaN
````

````
NaN
````

````julia
NaN == NaN
````

````
false
````

````julia
Inf > NaN
````

````
false
````

````julia
NaN - NaN
````

````
NaN
````

````julia
NaN in [NaN]
````

````
false
````

````julia
0.3 == 3 * 0.1
````

````
false
````

## Pregunta 018

Cree una matriz `5x5` con valores `[1, 2, 3, 4]` justo debajo de la diagonal. (★ ☆☆)

````julia
mA = diagm(5, 5, -1 => 1:4)
````

````
5×5 Matrix{Int64}:
 0  0  0  0  0
 1  0  0  0  0
 0  2  0  0  0
 0  0  3  0  0
 0  0  0  4  0
````

## Pregunta 019

Cree una matriz `8x8` y llénela con un patrón de tablero de ajedrez. (★ ☆☆)

````julia
mA = zeros(8, 8);
mA[2:2:end, 1:2:end] .= 1;
mA[1:2:end, 2:2:end] .= 1;
mA
````

````
8×8 Matrix{Float64}:
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
````

Por Tomer Arnon (https://github.com/tomerarnon):

````julia
mA = Int[isodd(ii + jj) for ii in 1:8, jj in 1:8];
````

## Pregunta 020

Convierta el índice lineal 100 a un _CartesianIndex_ de tamaño `(6,7,8)`. (★ ☆☆)

````julia
mA = rand(6, 7, 8);
cartIdx = CartesianIndices(mA)[100]; #<! See https://discourse.julialang.org/t/14666
mA[cartIdx] == mA[100]
````

````
true
````

## Pregunta 021

Cree una matriz `8x8` 8x8` usando la función `repeat()`.(★ ☆☆)

````julia
mA = repeat([0 1; 1 0], 4, 4)
````

````
8×8 Matrix{Int64}:
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
````

## Pregunta 022

Normalice una matriz aleatoria de `4x4`. (★ ☆☆)

````julia
mA = rand(4, 4);
mA .= (mA .- mean(mA)) ./ std(mA) #<! Pay attention that `@.` will yield error (`std()` and `mean()`)
````

````
4×4 Matrix{Float64}:
 -1.0589     0.696722    0.474169   0.0807478
  1.33922    1.23329    -0.559528  -1.24305
 -0.652489   0.919517    1.16875   -1.49035
 -0.0565761  0.0550669   0.711533  -1.61812
````

## Pregunta 023

Cree un _struct_ que describa un color como cuatro bytes sin signo (`RGBA`). (★ ☆☆)

````julia
struct sColor
    R::UInt8;
    G::UInt8;
    B::UInt8;
    A::UInt8;
end

sMyColor = sColor(rand(UInt8, 4)...)
````

````
Main.var"##312".sColor(0xb0, 0xae, 0x35, 0x81)
````

## Pregunta 024

Multiplique una matriz de `2x4` por una matriz de `4x3`. (★ ☆☆)

````julia
mA = rand(2, 4) * randn(4, 3)
````

````
2×3 Matrix{Float64}:
 -1.47402   -1.10919   -1.22996
 -0.745242   0.188422  -3.19746
````

## Pregunta 025

Dada una matriz 1D, niegue todos los elementos que están entre 3 y 8, en su lugar (in place). (★ ☆☆)

````julia
vA = rand(1:10, 8);
map!(x -> ((x > 3) && (x < 8)) ? -x : x, vA, vA)
````

````
8-element Vector{Int64}:
 -6
  3
  1
 -4
  3
 -4
 -5
 -4
````

Julia también permite la notación matemáticas (ver `P0027`):

````julia
vA = rand(1:10, 8);
map!(x -> 3 < x < 8 ? -x : x, vA, vA)
````

````
8-element Vector{Int64}:
 -7
 -6
 -4
  1
 -6
 10
  8
 -5
````

Usando índices lógicos:

````julia
vA[3 .< vA .< 8] .*= -1;
````

## Pregunta 026

Sume la matriz `1:4` con valor inicial de -10. (★ ☆☆)

````julia
sum(1:4, init = -10)
````

````
0
````

## Pregunta 027

Considere un vector de enteros `vz` y validar las siguientes expresiones. (★ ☆☆)

```julia
vZ .^ vZ
2 << vZ >> 2
vZ <- vZ
1im * vZ
vZ / 1 / 1
vZ < Z > Z
```

````julia
vZ = rand(1:10, 3);
````

````julia
vZ .^ vZ
````

````
3-element Vector{Int64}:
 387420489
 387420489
     46656
````

````julia
try
    2 << vZ >> 2
catch e
    println(e)
end
````

````
MethodError(<<, (2, [9, 9, 6]), 0x0000000000007f1f)

````

````julia
vZ <- vZ
````

````
false
````

````julia
1im * vZ
````

````
3-element Vector{Complex{Int64}}:
 0 + 9im
 0 + 9im
 0 + 6im
````

````julia
vZ / 1 / 1
````

````
3-element Vector{Float64}:
 9.0
 9.0
 6.0
````

````julia
vZ < vZ > vZ
````

````
false
````

## Pregunta 028

Evaluar las siguientes expresiones. (★ ☆☆)

````julia
[0] ./ [0]
````

````
1-element Vector{Float64}:
 NaN
````

````julia
try
    [0] .÷ [0]
catch e
    println(e)
end
````

````
DivideError()

````

````julia
try
    convert(Float, convert(Int, NaN))
catch e
    println(e)
end
````

````
InexactError(:Int64, Int64, NaN)

````

## Pregunta 029

Round away from zero a float array. (★☆☆)
Redondear una matriz de flotantes `vA` lejos del 0. (★☆☆)

````julia
vA = randn(10);
map(x -> x > 0 ? ceil(x) : floor(x), vA)
````

````
10-element Vector{Float64}:
  1.0
 -1.0
 -1.0
 -1.0
  2.0
 -1.0
  2.0
  2.0
  2.0
  1.0
````

## Pregunta 030

Encuentre los valores comunes entre dos matrices. (★ ☆☆)

````julia
vA = rand(1:10, 6);
vB = rand(1:10, 6);

vA[findall(in(vB), vA)]
````

````
2-element Vector{Int64}:
 7
 5
````

## Pregunta 031

Suprimir las advertencias ("warnings") de Julia. (★ ☆☆)

Uno puede usar [Suppressor.jl](https://github.com/JuliaIO/Suppressor.jl).

## Pregunta 032

Compare `sqrt(-1)` y `sqrt(-1 + 0im)`. (★ ☆☆)

````julia
try
    sqrt(-1)
catch e
    println(e)
end
````

````
DomainError(-1.0, "sqrt will only return a complex result if called with a complex argument. Try sqrt(Complex(x)).")

````

````julia
sqrt(-1 + 0im)
````

````
0.0 + 1.0im
````

## Pregunta 033

Muestra la fecha de ayer, hoy y de mañana usando `Dates`. (★ ☆☆)

````julia
println("Yesterday: $(today() - Day(1))");
println("Today: $(today())");
println("Tomorrow: $(today() + Day(1))");
````

````
Yesterday: 2022-10-26
Today: 2022-10-27
Tomorrow: 2022-10-28

````

## Pregunta 034

Muestre todas las fechas correspondientes al mes de julio de 2016. (★★ ☆)

````julia
collect(Date(2016,7,1):Day(1):Date(2016,7,31))
````

````
31-element Vector{Dates.Date}:
 2016-07-01
 2016-07-02
 2016-07-03
 2016-07-04
 2016-07-05
 2016-07-06
 2016-07-07
 2016-07-08
 2016-07-09
 2016-07-10
 2016-07-11
 2016-07-12
 2016-07-13
 2016-07-14
 2016-07-15
 2016-07-16
 2016-07-17
 2016-07-18
 2016-07-19
 2016-07-20
 2016-07-21
 2016-07-22
 2016-07-23
 2016-07-24
 2016-07-25
 2016-07-26
 2016-07-27
 2016-07-28
 2016-07-29
 2016-07-30
 2016-07-31
````

## Pregunta 035

Calcule `((mA + mB) * (-mA / 2))` de manera in place. (★★☆)

````julia
mA = rand(2, 2);
mB = rand(2, 2);
mA .= ((mA .+ mB) .* (.-mA ./ 2))
````

````
2×2 Matrix{Float64}:
 -0.35038   -0.685683
 -0.510546  -0.444504
````

Usando el macro "punto":

````julia
@. mA = ((mA + mB) * (-mA / 2));
````

## Pregunta 036

Extraiga la parte entera de una matriz aleatoria de números positivos utilizando 4 métodos diferentes. (★★ ☆)

````julia
mA = 5 * rand(3, 3);
````

Opción 1:

````julia
floor.(mA)
````

````
3×3 Matrix{Float64}:
 0.0  0.0  4.0
 2.0  3.0  4.0
 0.0  3.0  3.0
````

Opción2:


````julia
round.(mA .- 0.5) #<! Generates -0.0 for numbers smaller than 0.5
````

````
3×3 Matrix{Float64}:
  0.0  0.0  4.0
  2.0  3.0  4.0
 -0.0  3.0  3.0
````

Opción 3:

````julia
mA .÷ 1
````

````
3×3 Matrix{Float64}:
 0.0  0.0  4.0
 2.0  3.0  4.0
 0.0  3.0  3.0
````

Opción 4:

````julia
mA .- rem.(mA, 1)
````

````
3×3 Matrix{Float64}:
 0.0  0.0  4.0
 2.0  3.0  4.0
 0.0  3.0  3.0
````

## Pregunta 037

Cree una matriz `5x5` con valores de columna que van de 0 a 4. (★★ ☆)

````julia
mA = repeat(reshape(0:4, 1, 5), 5, 1)
````

````
5×5 Matrix{Int64}:
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
````

También se podría generar el rango de fila usando _transpose_ `'`:

````julia
mA = repeat((0:4)', 5, 1);
````

## Pregunta 038

Genere una matriz de 10 números utilizando un generador. (★ ☆☆)

````julia
vA = collect(x for x in 1:10)
````

````
10-element Vector{Int64}:
  1
  2
  3
  4
  5
  6
  7
  8
  9
 10
````

En Julia, el resultado de `collect` se puede lograr directamente utilizando una _Array Comprehension_ / _comprehensión de arreglo_:

````julia
vA = [x for x in 1:10];
````

## Pregunta 039

Cree un vector de tamaño 10 con valores que varían de 0 a 1, ambos excluidos. (★★ ☆)

````julia
vA = LinRange(0, 1, 12)[2:(end - 1)]
````

````
10-element LinRange{Float64, Int64}:
 0.0909091,0.181818,0.272727,0.363636,…,0.636364,0.727273,0.818182,0.909091
````

## Pregunta 040

Cree un vector aleatorio de tamaño 10 y ordénelo. (★★ ☆)

````julia
vA = rand(1:10, 10);
sort(vA) #<! Use `sort!()` for inplace sorting
````

````
10-element Vector{Int64}:
  1
  3
  3
  4
  4
  4
  7
  8
  9
 10
````

## Pregunta 041

Implemente la función `sum()` manualmente. (★★ ☆)

````julia
vA = rand(100);

function MySum(vA::Vector{T}) where{T <: Number}
sumVal = vA[1];
for ii in 2:length(vA)
    sumVal += vA[ii];
end

return sumVal;

end

MySum(vA)
````

````
51.34991384741698
````

## Pregunta 042

Verifique la igualdad de 2 matrices. (★★ ☆)

````julia
vA = rand(10);
vB = rand(10);

all(vA .== vB)
````

````
false
````

## Pregunta 043 TODO: Update

Haga una matriz inmutable (solo puede ser leída). (★★ ☆)


## Pregunta 044

Considere una matriz `10x2` aleatoria que representa las coordenadas cartesianas, conviértalas en coordenadas polares. (★★ ☆)

````julia
mA = rand(10, 2);

ConvToPolar = vX -> [hypot(vX[1], vX[2]), atan(vX[2], vX[1])]

mB = [ConvToPolar(vX) for vX in eachrow(mA)]
````

````
10-element Vector{Vector{Float64}}:
 [0.9505364569557584, 0.031648622825633764]
 [0.704392126760974, 0.5147716023358581]
 [0.29679995764188105, 1.201649642883764]
 [0.637435149299262, 0.02987122275134911]
 [0.933745980010277, 0.7244055260446777]
 [0.9187482092583683, 0.36651502794834323]
 [1.0164226188075605, 0.9581226557842126]
 [0.5946171056720952, 1.4392243895565575]
 [0.7889136757232136, 0.2964469880257975]
 [1.044698619009772, 0.8754548962664869]
````

Para tener el mismo tamaño de salida:

````julia
mC = reduce(hcat, mB)';
````

## Pregunta 045

Cree un vector aleatorio de tamaño 10 y reemplace el valor máximo por 0. (★★ ☆)

````julia
vA = randn(10);
````

En caso de un solo máximo o todos los valores diferentes:

````julia
vA[argmax(vA)] = 0;
vA
````

````
10-element Vector{Float64}:
  0.15593661212531384
  0.8177229521444311
 -1.4850097210409072
  0.0
  0.8552383451908633
  1.476127811761641
  0.2407698166125247
 -0.6363509339561092
 -0.5514594178114751
  0.8756142494364301
````

Solución general:

````julia
maxVal = maximum(vA);
vA .= (valA == maxVal ? 0 : valA for valA in vA); #<! Non allocating generator by using `.=`
````

## Pregunta 046

Cree una cuadrícula de coordenadas `x` y `y` que cubran el área `[0, 1] x [0, 1]`. (★★ ☆)

````julia
numGridPts = 5;
vX = LinRange(0, 1, numGridPts);
vY = LinRange(0, 1, numGridPts);
MeshGrid = (vX, vY) -> ([x for _ in vY, x in vX], [y for y in vY, _ in vX]);

mX, mY = MeshGrid(vX, vY); #<! Ver https://discourse.julialang.org/t/48679
@show mX
````

````
5×5 Matrix{Float64}:
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
````

````julia
@show mY
````

````
5×5 Matrix{Float64}:
 0.0   0.0   0.0   0.0   0.0
 0.25  0.25  0.25  0.25  0.25
 0.5   0.5   0.5   0.5   0.5
 0.75  0.75  0.75  0.75  0.75
 1.0   1.0   1.0   1.0   1.0
````

Por [Tomer Arnon](https://github.com/tomerarnon):

````julia
mXY = [(ii, jj) for ii in 0:0.25:1, jj in 0:0.25:1]; #<! Also `tuple.(0:0.25:1, (0:0.25:1)')`
````

## Pregunta 047

Dados dos vectores, `vx` y` vy`, construye la matriz de Cauchy `mc`:` (c_ij = 1 / (xi - yj)) `. (★★ ☆)

````julia
vX = rand(5);
vY = rand(5);

mC = 1 ./ (vX .- vY')
````

````
5×5 Matrix{Float64}:
 21.646    3.23455  34.1025   3.79522  -3.10044
 12.1532   2.89647  15.2886   3.33807  -3.49101
  5.11271  2.18076   5.59545  2.422    -5.77562
 27.6005   3.34229  51.6618   3.94442  -3.00751
  2.36374  1.45768   2.46193  1.56164  18.4072
````

## Pregunta 048

Imprima el valor mínimo y máximo representable para cada tipo escalar Julia. (★★ ☆)

````julia
vT = [UInt8 UInt16 UInt32 UInt64 Int8 Int16 Int32 Int64 Float16 Float32 Float64]

for juliaType in vT
    println(typemin(juliaType));
    println(typemax(juliaType));
end
````

````
0
255
0
65535
0
4294967295
0
18446744073709551615
-128
127
-32768
32767
-2147483648
2147483647
-9223372036854775808
9223372036854775807
-Inf
Inf
-Inf
Inf
-Inf
Inf

````

## Pregunta 049

Imprima todos los valores de una matriz. (★★ ☆)

````julia
mA = rand(3, 3);
print(mA);
````

````
[0.6807535316053605 0.849791747148149 0.32690265736495716; 0.9773227682466125 0.5276250185081583 0.9071015474523568; 0.3192975731085147 0.009594822627075117 0.21726819354916904]
````

## Pregunta 050

Encuentre el valor más cercano a un escalar dado en un vector. (★★ ☆)

````julia
inputVal = 0.5;
vA = rand(10);

vA[argmin(abs.(vA .- inputVal))]
````

````
0.5023858297186229
````

Por [Tomer Arnon](https://github.com/tomerarnon):

````julia
function MasCercano(vA::Vector{T}, inputVal::T) where{T <: Number}
    return argmin(y -> abs(y - inputVal), vA);
end

MasCercano(vA, inputVal)
````

````
0.5023858297186229
````

## Pregunta 051

Cree una matriz estructurada que represente una posición `(x, y)` y un color `(r, g, b)`. (★★ ☆)

````julia
struct sPosColor
    x::Int
    y::Int
    R::UInt8;
    G::UInt8;
    B::UInt8;
    A::UInt8;
end

numPixels   = 10;
maxVal      = typemax(UInt32);
vMyColor    = [sPosColor(rand(1:maxVal, 2)..., rand(UInt8, 4)...) for _ in 1:numPixels];
````

## Pregunta 052

Considere un vector aleatorio de forma `(5, 2)` que representa coordenadas. Encuentre la matriz de distancias `mD`: ${D}_{i, j} = {\left\| {x}_{i} - {x}_{j}\right\|}_{2} $. (★★ ☆)

````julia
mX = rand(5, 2);
vSumSqr = sum(vX -> vX .^ 2, mX, dims = 2);
mD = vSumSqr .+ vSumSqr' - 2 * (mX * mX');
mD #<! Apply `sqrt.()` for the actual norm
````

````
5×5 Matrix{Float64}:
 -4.44089e-16  0.135171   0.729876     0.724544   0.525945
  0.135171     0.0        0.539868     0.255352   0.136451
  0.729876     0.539868  -1.38778e-17  0.403845   0.814356
  0.724544     0.255352   0.403845     0.0        0.135001
  0.525945     0.136451   0.814356     0.135001  -4.44089e-16
````

## Pregunta 053

Convierta una matriz flotante (32 bits) en un entero (32 bits) en su lugar. (★★ ☆)

````julia
vA = 9999 .* rand(Float32, 5);
vB = reinterpret(Int32, vA); #<! Creates a view
@. vB = trunc(Int32, vA) #<! Updates the byes in th view (Inplace for `vA`)
````

````
5-element reinterpret(Int32, ::Vector{Float32}):
 8898
 1815
 6821
 6523
 9953
````

Lo anterior es equivalente a:
```julia
for ii in eachindex(vB)
    vB[ii] = trunc(Int32, vA[ii]);
end
vB
```

## Pregunta 054

Lea el siguiente archivo: (`Q0054.txt`). (★★☆)
```
1, 2, 3, 4, 5
6,  ,  , 7, 8
 ,  , 9,10,11
```

````julia
mA = readdlm("Q0054.txt", ',')
````

````
3×5 Matrix{Any}:
 1     2      3       4   5
 6      "  "   "  "   7   8
  " "   "  "  9      10  11
````

## Pregunta 055

Enumerar una matriz con un bucle. (★★☆)

````julia
mA = rand(3, 3);

for (elmIdx, elmVal) in enumerate(mA) #<! See https://discourse.julialang.org/t/48877
    println(elmIdx);
    println(elmVal);
end
````

````
1
0.7028850425818378
2
0.9169645026836734
3
0.887675432103485
4
0.6988267487719038
5
0.7143993871851885
6
0.8303140449034555
7
0.43387559304673373
8
0.13163225199507878
9
0.6590727215475687

````

## Pregunta 056

Genere una matriz Gaussiana 2D genérica con `μ = 0`, `σ = 1` e índices sobre `{-5, -4, ..., 0, 1, ..., 5}`. (★★ ☆)

````julia
vA = -5:5;
μ = 0;
σ = 1;
mG = [(1 / (2 * pi * σ)) * exp(-0.5 * ((([x, y] .- μ)' * ([x, y] .- μ)) / (σ * σ))) for x in vA, y in vA];

heatmap(mG)
````

````
      ┌───────────┐              
   11 │▄▄▄▄▄▄▄▄▄▄▄│  ┌──┐ 0.2    
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
    1 │▄▄▄▄▄▄▄▄▄▄▄│  └──┘ 2.0e-12
      └───────────┘              
       1        11               
````

Usando la separabilidad de la función gaussiana:

````julia
vG = (1 / (sqrt(2 * pi) * σ)) .* exp.(-0.5 .* (((vA .- μ) .^ 2) / (σ * σ)));
mG = vG * vG';
````

## Pregunta 057

Coloque 5 elementos en una matriz `5x5` al azar. (★★ ☆)

````julia
mA = rand(5, 5);
mA[rand(1:25, 5)] = rand(5);
````

Otra opción que evita repetir índices:

````julia
mA[randperm(25)[1:5]] = rand(5);
````

## Pregunta 058

Resta la media de cada fila de una matriz. (★★ ☆)

````julia
mA = rand(3, 3);
mA .-= mean(mA, dims = 2);
mean(mA, dims = 1)
````

````
1×3 Matrix{Float64}:
 0.261517  -0.0218978  -0.23962
````

## Pregunta 059

Ordene una matriz por una columna. (★★ ☆)

````julia
colIdx = 2;

mA = rand(3, 3);
mA[sortperm(mA[:, colIdx]), :]
````

````
3×3 Matrix{Float64}:
 0.870197  0.229455  0.462788
 0.812345  0.61344   0.0990058
 0.271644  0.722126  0.182457
````

Usando `sortslices()`:

````julia
sortslices(mA, dims = 1, by = x -> x[colIdx]);
````

## Pregunta 060

Encontrar si una matriz 2D dada tiene columnas nulas (todas ceros). (★★ ☆)

````julia
mA = rand(0:1, 3, 9);
any(all(iszero.(mA), dims = 1))
````

````
false
````

## Pregunta 061

Encuentre el segundo valor más cercano de un valor dado en una matriz. (★★ ☆)

````julia
inputVal = 0.5;
vA = rand(10);

vA[sortperm(abs.(vA .- inputVal))[2]]
````

````
0.5947029703004421
````

Alternative form (more efficient)

````julia
closeFirst  = Inf;
closeSecond = Inf;
closeFirstIdx  = 0;
closeSecondIdx = 0;

# usando scope/alcance global en Literate.jl:
for (elmIdx, elmVal) in enumerate(abs.(vA .- inputVal))
    if (elmVal < closeFirst)
        global closeSecond = closeFirst;
        global closeFirst = elmVal;
        global closeSecondIdx  = closeFirstIdx;
        global closeFirstIdx   = elmIdx;
    elseif (elmVal < closeSecond)
        global closeSecond = elmVal;
        global closeSecondIdx = elmIdx;
    end
end

vA[closeSecondIdx] == vA[sortperm(abs.(vA .- inputVal))[2]]
````

````
true
````

Por [Tomer Arnon](https://github.com/tomerarnon):

````julia
vA[partialsortperm(abs.(vA .- inputVal), 2)]
````

````
0.5947029703004421
````

## Pregunta 062

Teniendo en cuenta dos matrices con forma `(1, 3)` y `(3, 1)`, calcule su suma usando un iterador. (★★ ☆)

````julia
vA = rand(1, 3);
vB = rand(3, 1);

sum(aVal + bVal for aVal in vA, bVal in vB)
````

````
11.149909948305584
````

## Pregunta 063

Cree una tipo de matriz que tenga un atributo de nombre. (★★ ☆)

Puedes usar `NamedArrays.jl` o `AxisArrays.jl`.

## Pregunta 064

Dado un vector, agregue `1` a cada elemento indexado por un segundo vector (tenga cuidado con los índices repetidos). (★★★)

````julia
vA = rand(1:10, 5);
vB = rand(1:5, 3);

println(vA);

# Julia es muy eficiente con los bucles!
for bIdx in vB
    vA[bIdx] += 1;
end

println(vA);
````

````
[1, 6, 2, 6, 2]
[3, 7, 2, 6, 2]

````

## Pregunta 065

Acumular elementos de un vector `x` a una matriz `f` basada en una lista de índices 'I'. (★★★)

````julia
vX = rand(1:5, 10);
vI = rand(1:15, 10);

numElements = maximum(vI);
vF = zeros(numElements);

for (ii, iIdx) in enumerate(vI)
    vF[iIdx] += vX[ii];
end

println("vX: $vX");
println("vI: $vI");
println("vF: $vF");
````

````
vX: [5, 4, 3, 5, 2, 5, 2, 5, 5, 1]
vI: [3, 2, 6, 11, 12, 10, 5, 11, 12, 2]
vF: [0.0, 5.0, 5.0, 0.0, 2.0, 3.0, 0.0, 0.0, 0.0, 5.0, 10.0, 7.0]

````

También se podría usar `counts()` de `StatsSase.jl`.

## Pregunta 066

Teniendo en cuenta una imagen de la imagen de tamaño `w x h x 3` del tipo `UInt8`, calcule el número de colores únicos. (★★ ☆)

````julia
mI = rand(UInt8, 1000, 1000, 3);

numColors = length(unique([reinterpret(UInt32, [iPx[1], iPx[2], iPx[3], 0x00])[1] for iPx in eachrow(reshape(mI, :, 3))])); #<! Reshaping as at the moment `eachslice()` doesn't support multiple `dims`.
print("Number of Unique Colors: $numColors");
````

````
Number of Unique Colors: 970711
````

Otra opción:

````julia
numColors = length(unique([UInt32(iPx[1]) + UInt32(iPx[2]) << 8 + UInt32(iPx[3]) << 16 for iPx in eachrow(reshape(mI, :, 3))]));
print("Number of Unique Colors: $numColors");
````

````
Number of Unique Colors: 970711
````

Forma más simple de slicear un píxel:

````julia
numColors = length(unique([UInt32(mI[ii, jj, 1]) + UInt32(mI[ii, jj, 2]) << 8 + UInt32(mI[ii, jj, 3]) << 16 for ii in 1:size(mI, 1), jj in 1:size(mI, 2)]));
print("Number of Unique Colors: $numColors");
````

````
Number of Unique Colors: 970711
````

## Pregunta 067

Teniendo en cuenta una matriz de cuatro dimensiones, obtenga una suma sobre los dos últimos ejes a la vez. (★★★)

````julia
mA = rand(2, 2, 2, 2);
sum(reshape(mA, (2, 2, :)), dims = 3)
````

````
2×2×1 Array{Float64, 3}:
[:, :, 1] =
 1.817    1.16234
 2.44291  2.32796
````

## Pregunta 068

Teniendo en cuenta un vector `VA` unidimensional, muestra cómo calcular los promedios de subconjuntos de 'VA` utilizando un vector `VS` del mismo tamaño que describe los índices de subconjunto. (★★★)
Considering a one dimensional vector `vA`, how to compute means of subsets of `vA` using a vector `vS` of same size describing subset indices. (★★★)

````julia
# Básicamente extendiendo `Q0065` con otro vector de número de adiciones.

vX = rand(1:5, 10);
vI = rand(1:15, 10);

numElements = maximum(vI);
vF = zeros(numElements);
vN = zeros(Int, numElements);

for (ii, iIdx) in enumerate(vI)
    vF[iIdx] += vX[ii];
    vN[iIdx] += 1;
end

# We only divide the mean if the number of elements accumulated is bigger than 1
for ii in 1:numElements
    vF[ii] = ifelse(vN[ii] > 1, vF[ii] / vN[ii], vF[ii]);
end

println("vX: $vX");
println("vI: $vI");
println("vF: $vF");
````

````
vX: [5, 5, 4, 2, 1, 1, 3, 5, 3, 2]
vI: [14, 7, 8, 10, 5, 10, 14, 2, 7, 13]
vF: [0.0, 5.0, 0.0, 0.0, 1.0, 0.0, 4.0, 4.0, 0.0, 1.5, 0.0, 0.0, 2.0, 4.0]

````

## Pregunta 069

Obtenga la diagonal de un producto de matriz. (★★★)

````julia
mA = rand(5, 7);
mB = rand(7, 4);

numDiagElements = min(size(mA, 1), size(mB, 2));
vD = [dot(mA[ii, :], mB[:, ii]) for ii in 1:numDiagElements]
````

````
4-element Vector{Float64}:
 1.8937792321469207
 1.035584608236753
 2.0251852803210024
 2.2065505485118653
````

Forma alternativa:

````julia
vD = reshape(sum(mA[1:numDiagElements, :]' .* mB[:, 1:numDiagElements], dims = 1), numDiagElements)
````

````
4-element Vector{Float64}:
 1.8937792321469207
 1.035584608236753
 2.0251852803210024
 2.2065505485118653
````

## Pregunta 070
Considere el vector `[1, 2, 3, 4, 5]`, construya un nuevo vector con 3 ceros consecutivos intercalados entre cada valor. (★★★)

````julia
vA = 1:5;

# Dado que Julia es rápida con los bucles, sería la elección más fácil:

numElements = (4 * length(vA)) - 3;
vB = zeros(Int, numElements);

for (ii, bIdx) in enumerate(1:4:numElements)
    vB[bIdx] = vA[ii];
end
println(vB);

# Alternative (MATLAB style) way:

mB = [reshape(collect(vA), 1, :); zeros(Int, 3, length(vA))];
vB = reshape(mB[1:(end - 3)], :);
println(vB);
````

````
[1, 0, 0, 0, 2, 0, 0, 0, 3, 0, 0, 0, 4, 0, 0, 0, 5]
[1, 0, 0, 0, 2, 0, 0, 0, 3, 0, 0, 0, 4, 0, 0, 0, 5]

````

## Pregunta 071

Considere una matriz de dimensión `5 x 5 x 3`, mulitpliquela por una matriz con dimensiones `5 x 5` usando `broadcasting`. (★★★)

````julia
mA = rand(5, 5, 3);
mB = rand(5, 5);

mA .* mB #<! Very easy in Julia
````

````
5×5×3 Array{Float64, 3}:
[:, :, 1] =
 0.492335  0.301617  0.0158155   0.411494  0.0331824
 0.555254  0.148368  0.111992    0.366332  0.192798
 0.104442  0.249306  0.0138448   0.018588  0.721434
 0.665075  0.136419  0.00305929  0.430373  0.208216
 0.290075  0.642668  0.519127    0.511527  0.151719

[:, :, 2] =
 0.234647   0.447608  0.000903852  0.00299349  0.0626502
 0.0159529  0.164814  0.0807125    0.27415     0.180858
 0.103613   0.291711  0.00759939   0.013771    0.11713
 0.314552   0.210101  0.00966737   0.343302    0.377711
 0.129541   0.642804  0.833245     0.372239    0.816422

[:, :, 3] =
 0.774094  0.181579   0.0151706   0.26963    0.0364216
 0.167574  0.0016081  0.0130672   0.823491   0.398857
 0.062678  0.40945    0.00790564  0.0141378  0.468662
 0.344903  0.18419    0.00697708  0.487335   0.504131
 0.118821  0.0130137  0.803091    0.754898   0.0470187
````

## Pregunta 072

Intercambie dos filas de una matriz 2D. (★★★)

````julia
mA = rand(UInt8, 3, 2);
println(mA);
mA[[1, 2], :] .= mA[[2, 1], :];
println(mA);
````

````
UInt8[0xc7 0x2f; 0xbf 0x8f; 0xac 0x2a]
UInt8[0xbf 0x8f; 0xc7 0x2f; 0xac 0x2a]

````

## Pregunta 073

Considere un conjunto de 10 tripletas que describen 10 triángulos (con vértices compartidos), encuentre el conjunto de segmentos de línea únicos que componen todos los triángulos. (★★★)

````julia
mA = rand(0:100, 10, 3); #<! Each row composes 3 veritces ([1] -> [2], [2] -> [3], [3] -> [1])
mC = [sort!([vC[mod1(ii, end)], vC[mod1(ii + 1, end)]]) for ii in 1:(size(mA, 2) + 1), vC in eachrow(mA)][:] #<! Sorted combinations of vertices
mC = unique(mC)
````

````
30-element Vector{Vector{Int64}}:
 [52, 86]
 [23, 86]
 [23, 52]
 [53, 88]
 [53, 95]
 [88, 95]
 [4, 31]
 [4, 24]
 [24, 31]
 [34, 80]
 [34, 99]
 [80, 99]
 [19, 69]
 [19, 21]
 [21, 69]
 [38, 74]
 [36, 74]
 [36, 38]
 [18, 20]
 [20, 48]
 [18, 48]
 [0, 23]
 [23, 77]
 [0, 77]
 [23, 42]
 [42, 75]
 [23, 75]
 [20, 69]
 [7, 69]
 [7, 20]
````

## Pregunta 074

Dada una matriz ordenada `VC` que corresponde a un bindount, produce una matriz `VA` tal que `bincount(VA) == VC`. (★★★)

````julia
vC = rand(0:7, 5);
numElements = sum(vC);
vA = zeros(Int, numElements);

elmIdx = 1;
# Usando `global` para alcance en alfabetizado
for (ii, binCount) in enumerate(vC)
    for jj in 1:binCount
        vA[elmIdx] = ii;
        global elmIdx += 1;
    end
end
````

## Pregunta 075

Calcule promedios utilizando una ventana deslizante sobre una matriz. (★★★)

````julia
numElements = 10;
winRadius   = 1;
winReach    = 2 * winRadius;
winLength   = 1 + winReach;

vA = rand(0:3, numElements);
vB = zeros(numElements - (2 * winRadius));

aIdx = 1 + winRadius;
# Usando `global` para alcance en alfabetizado
for ii in 1:length(vB)
    vB[ii] = mean(vA[(aIdx - winRadius):(aIdx + winRadius)]); #<! Using integral / running sum it would be faster.
    global aIdx += 1;
end
````

Otro método que usa la suma corriente:

````julia
vC = zeros(numElements - winReach);

jj = 1;
sumVal = sum(vA[1:winLength]);
vC[jj] = sumVal / winLength;
jj += 1;

# Usando `global` para alcance en alfabetizado
for ii in 2:(numElements - winReach)
    global sumVal += vA[ii + winReach] - vA[ii - 1];
    vC[jj] = sumVal / winLength;
    global jj += 1;
end

maximum(abs.(vC - vB)) < 1e-8
````

````
true
````

## Pregunta 076

Considere una matriz unidimensional `VA`, construya una matriz bidimensional cuya primera fila es `[VA [0], VA [1], VA [2]]` y cada fila posterior se desplaza por 1. (★★★)

````julia
vA = rand(10);
numCols = 3;

numRows = length(vA) - numCols + 1;
mA = zeros(numRows, numCols);

for ii in 1:numRows
    mA[ii, :] = vA[ii:(ii + numCols - 1)]; #<! One could optimize the `-1` out
end
````

## Pregunta 077

Niega un booleano o  multiplica por `-1` para cambiar el valor de un número de manera in place.

````julia
vA = rand(Bool, 10);
vA .= .!vA;

vA = randn(10);
vA .*= -1;
````

## Pregunta 078

Considere 2 conjuntos de puntos `mp1`,`mp2` describiendo líneas en 2D y un punto `vp`. Calcula la distancia desde el punto `vP` a cada línea `i`:` [mp1[i,:], mp2[i,:]]`. (★★★)

````julia
# Ver distancia de un punto desde una línea en Wikipedia (https://en.wikipedia.org/wiki/distance_from_a_point_to_a_line).
# Específicamente _line definido por dos puntos_.

numLines = 10;
mP1 = randn(numLines, 2);
mP2 = randn(numLines, 2);
vP  = randn(2);

vD = [(abs(((vP2[1] - vP1[1]) * (vP1[2] - vP[2])) - ((vP1[1] - vP[1]) * (vP2[2] - vP1[2]))) / hypot((vP2 - vP1)...)) for (vP1, vP2) in zip(eachrow(mP1), eachrow(mP2))];
minDist = minimum(vD);

println("Min Distance: $minDist");
````

````
Min Distance: 0.42811311783896533

````

## Pregunta 079

Considere 2 conjuntos de puntos `mP1`, `mP2` que describan líneas 2D y un conjunto de puntos `mp`, calcular la distancia desde el punto `vp = mp[j,:]` a cada línea `i`: `[mp1[i,:], mp2[i,:]]`. (★★★)

````julia
numLines = 5;
mP1 = randn(numLines, 2);
mP2 = randn(numLines, 2);
mP  = randn(numLines, 2);

mD = [(abs(((vP2[1] - vP1[1]) * (vP1[2] - vP[2])) - ((vP1[1] - vP[1]) * (vP2[2] - vP1[2]))) / hypot((vP2 - vP1)...)) for (vP1, vP2) in zip(eachrow(mP1), eachrow(mP2)), vP in eachrow(mP)];

for jj in 1:numLines
    minDist = minimum(mD[jj, :]);
    println("The minimum distance from the $jj -th point: $minDist");
end
````

````
┌ Warning: Assignment to `minDist` in soft scope is ambiguous because a global variable by the same name exists: `minDist` will be treated as a new local. Disambiguate by using `local minDist` to suppress this warning or `global minDist` to assign to the existing global variable.
└ @ string:9
The minimum distance from the 1 -th point: 0.33333028326949365
The minimum distance from the 2 -th point: 0.09596286876613971
The minimum distance from the 3 -th point: 0.15987404532559377
The minimum distance from the 4 -th point: 0.09922388894592074
The minimum distance from the 5 -th point: 0.0701461047753776

````

## Pregunta 080

Considere una matriz 2D arbitraria, escriba una función que extraiga una subparte con una forma fija y se centre en un elemento dado (Handel fuera de los límites). (★★★)

````julia
# Uno podría usar `paddedviews.jl` para resolverlo fácilmente.

arrayLength = 10;
winRadius   = 3;
vWinCenter  = [7, 9];

mA = rand(arrayLength, arrayLength);
winLength = (2 * winRadius) + 1;
mB = zeros(winLength, winLength);

verShift = -winRadius;
# Usando `global` para alcance en alfabetizado
for ii in 1:winLength
    horShift = -winRadius;
    for jj in 1:winLength
        mB[ii, jj] = mA[min(max(vWinCenter[1] + verShift, 1), arrayLength), min(max(vWinCenter[2] + horShift, 1), arrayLength)]; #<! Nearest neighbor extrapolation
        horShift += 1;
    end
    global verShift += 1;
end
````

## Pregunta 081

Considere una matriz `VA = [1, 2, 3, ..., 13, 14]`, genere una matriz `vb = [[1, 2, 3, 4], [2, 3, 4, 5], [3, 4, 5, 6], ..., [11, 12, 13, 14]] `.. (★★★)

````julia
vA = collect(1:14);

winNumElements  = 4;
winReach        = winNumElements - 1;

vB = [vA[ii:(ii + winReach)] for ii in 1:(length(vA) - winReach)]
````

````
11-element Vector{Vector{Int64}}:
 [1, 2, 3, 4]
 [2, 3, 4, 5]
 [3, 4, 5, 6]
 [4, 5, 6, 7]
 [5, 6, 7, 8]
 [6, 7, 8, 9]
 [7, 8, 9, 10]
 [8, 9, 10, 11]
 [9, 10, 11, 12]
 [10, 11, 12, 13]
 [11, 12, 13, 14]
````

## Pregunta 082

Calcule un rango de matriz. (★★★)

````julia
numRows = 5;
numCols = 4;
mA = randn(numRows, numCols);
rank(mA)
````

````
4
````

## Pregunta 083

Find the most frequent value in an array. (★★★)

````julia
vA = rand(1:5, 15);
````

MATLAB Style (Manual loop might be faster)

````julia
vB = unique(vA);
# vb[argMax(suma(VA.==vb', dims = 1)[:])] # <! La entrada a `argMax ()` es un vector `1 x n`, por lo tanto, se reduce su ultima dimension, por lo que `argmax()` no devolverá el índice cartesiano.
````

````
1
````

Comparación de bits:

Uno podría convertirse en el nivel de bits a enteros y luego usar algo como `counts()` de `StatsBase.jl`.
Con 1 a 4 bytes de datos:
```julia
numBytes = sizeof(vA[1]);
if (sizeof(vA[1]) == 1)
    vB = reinterpret(UInt8, vA);
elseif (sizeof(vA[1]) == 2)
    vB = reinterpret(UInt16, vA);
elseif (sizeof(vA[1]) == 4)
    vB = reinterpret(UInt32, vA);
elseif (sizeof(vA[1]) == 8)
    vB = reinterpret(UInt64, vA);
end
```

## Pregunta 084

Extraiga todos los bloques `3x3` contiguos de una matriz `5x5` aleatoria. (★★★)

````julia
numRows = 5;
numCols = 5;

mA = rand(1:9, numRows, numCols);

winRadius   = 1;
winReach    = 2 * winRadius;
winLength   = winReach + 1;

mB = [mA[ii:(ii + winReach), jj:(jj + winReach)] for ii in 1:(numRows - winReach), jj in 1:(numCols - winReach)]
````

````
3×3 Matrix{Matrix{Int64}}:
 [9 1 1; 3 1 2; 9 4 6]  [1 1 4; 1 2 2; 4 6 2]  [1 4 7; 2 2 1; 6 2 2]
 [3 1 2; 9 4 6; 4 2 1]  [1 2 2; 4 6 2; 2 1 7]  [2 2 1; 6 2 2; 1 7 1]
 [9 4 6; 4 2 1; 2 9 8]  [4 6 2; 2 1 7; 9 8 1]  [6 2 2; 1 7 1; 8 1 4]
````

## Pregunta 085

Cree una estructura de matriz 2D tal que `ma[i, j] == ma[j, i]` (es una matriz simétrica). (★★★)

````julia
struct SymmetricMatrix{T <: Number} <: AbstractArray{T, 2}
    numRows::Int
    data::Matrix{T}

    function SymmetricMatrix(mA::Matrix{T}) where {T <: Number}
        size(mA, 1) == size(mA, 2) || throw(ArgumentError("Input matrix must be square"))
        new{T}(size(mA, 1), Matrix(Symmetric(mA)));
    end

end

function Base.size(mA::SymmetricMatrix)
    (mA.numRows, mA.numRows);
end
function Base.getindex(mA::SymmetricMatrix, ii::Int)
    mA.data[ii];
end
function Base.getindex(mA::SymmetricMatrix, ii::Int, jj::Int)
    mA.data[ii, jj];
end
function Base.setindex!(mA::SymmetricMatrix, v, ii::Int, jj::Int)
    setindex!(mA.data, v, ii, jj);
    setindex!(mA.data, v, jj, ii);
end

mA = SymmetricMatrix(zeros(Int, 2, 2));
mA[1, 2] = 5;
mA
````

````
2×2 Main.var"##312".SymmetricMatrix{Int64}:
 0  5
 5  0
````

## Pregunta 086

Considere un conjunto de matrices `P` de forma `nxn` y un conjunto de vectores `P` con longitud `n`. Calcule la suma de los productos vectoriales de matriz `P` a la vez (el resultado es un vector de longitud `n`). (★★★)

````julia
# Uno podría usar `tensoroperations.jl` o` einsum.jl` para una solución más elegante.

numRows = 5;
numMat  = 3;

tP = [randn(numRows, numRows) for _ in 1:numMat];
mP = [randn(numRows) for _ in 1:numMat];

vA = reduce(+, (mP * vP for (mP, vP) in zip(tP, mP)));
````

````julia
vB = zeros(numRows);
for ii in 1:numMat
    vB .+= tP[ii] * mP[ii];
end

vA == vB
````

````
true
````

## Pregunta 087

Considere una matriz `16x16`, calcule la suma del bloque (el tamaño del bloque es `4x4`). (★★★)

Resolvemos un caso más general para cualquier tamaño de bloques.

````julia
numRows = 16;
numCols = 8;

vBlockSize = [2, 4]; #<! [numRows, numCols] ./ vBlockSize == integer

mA = rand(numRows, numCols);

numBlocksVert   = numRows ÷ vBlockSize[1];
numBlocksHori   = numCols ÷ vBlockSize[2];
numBlocks       = numBlocksVert * numBlocksHori;

mA = reshape(mA, vBlockSize[1], :);
````

Numeramos la columna de bloques en cuanto a la columna y creamos su índice de bloque por columna del `Ma` reestructurado.

````julia
vBlockIdx = 1:numBlocks;
mBlockIdx = reshape(vBlockIdx, numBlocksVert, numBlocksHori);
mBlockIdx = repeat(mBlockIdx, 1, 1, vBlockSize[2]);
mBlockIdx = permutedims(mBlockIdx, (1, 3, 2));
vBlockIdx = mBlockIdx[:]; #<! Matches the block index per column of the reshaped `mA`.

vA = dropdims(sum(mA, dims = 1), dims = 1);
vB = zeros(numBlocks);

for ii = 1:(numBlocks * vBlockSize[2])
    vB[vBlockIdx[ii]] += vA[ii];
end
vB
````

````
16-element Vector{Float64}:
 4.354231620225193
 3.734856822720345
 3.297606250613403
 4.256409222766379
 3.2941384563138993
 3.776165923653995
 3.600353929303568
 4.518180088610547
 3.6679777425586186
 4.6420262282688345
 4.296040312870272
 5.1547123230902825
 3.0214360614973477
 3.202315920090961
 4.669003591708878
 3.3257368418156616
````

## Pregunta 088

Implemente la simulación del _Juego de la Vida_ usando matrices. (★★★)

````julia
numRows = 20;
numCols = 20;

gofKernel           = @kernel w -> w[-1, -1] + w[-1, 0] + w[-1, 1] + w[0, -1] + w[0, 1] + w[1, -1] + w[1, 0] + w[1, 1];
gofNumLives         = round(Int, 0.05 * numRows * numCols);
gofNumGenerations   = 50;

vI = randperm(numRows * numCols)[1:gofNumLives];

mG = zeros(UInt8, numRows, numCols);
mG[vI] .= UInt8(1);
mB = similar(mG);

heatmap(mG) #<! Initialización
````

````
      ┌────────────────────┐        
   20 │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  ┌──┐ 1
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
    1 │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  └──┘ 0
      └────────────────────┘        
       1                 20         
````

````julia
for ii in 1:numGridPts
    map!(gofKernel, mB, extend(mG, StaticKernels.ExtensionConstant(0))); #<! One may use `ExtensionCircular`
    for ii in eachindex(mB)
        mG[ii] = UInt8((mB[ii] >= 3) || ((mB[ii] > 0) && (mB[ii] == 2))); #<! Could be done with broadcasting
    end
end

heatmap(mG) #<! Final state
````

````
      ┌────────────────────┐        
   20 │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  ┌──┐ 1
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
      │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│  
    1 │▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│  └──┘ 0
      └────────────────────┘        
       1                 20         
````

TODO: Use la implementación O(1) para el Box Blur.

## Pregunta 089

Obtenga el valor más grande de una matriz. (★★★)

````julia
vA = rand(10);
numValues = 3;

vA[partialsortperm(vA, 1:numValues, rev = true)]
````

````
3-element Vector{Float64}:
 0.8713271882275592
 0.8486847944348448
 0.8445471427655805
````

## Pregunta 090

Dado un número arbitrario de vectores, construya el _producto cartesiano_ (para cada combinación de cada elemento). (★★★)

````julia
function CartesianProduct(tupleX)
    return collect(Iterators.product(tupleX...))[:];
end

vA = 1:3;
vB = 8:9;
vC = 4:5;

CartesianProduct((vA, vB, vC))
````

````
12-element Vector{Tuple{Int64, Int64, Int64}}:
 (1, 8, 4)
 (2, 8, 4)
 (3, 8, 4)
 (1, 9, 4)
 (2, 9, 4)
 (3, 9, 4)
 (1, 8, 5)
 (2, 8, 5)
 (3, 8, 5)
 (1, 9, 5)
 (2, 9, 5)
 (3, 9, 5)
````

## Pregunta 091

Cree una matriz a la que se pueda acceder como una matriz de registros en Numpy. (★★★)

Se puede usar `StructArrays.jl`.

## Pregunta 092

Considere un gran vector `VA`, calcule 'VA` elevado (cada elemento) a la 3ra potencia utilizando 3 métodos diferentes. (★★★)

````julia
vA = rand(1000);
````

Método 001:

````julia
vB = vA .^ 3;
````

Método 002:

````julia
vC = [valA ^ 3 for valA in vA];
````

Método 003:

````julia
vD = zeros(length(vA));
for (ii, valA) in enumerate(vA)
    vD[ii] = valA * valA * valA;
end
````

````julia
vB ≈ vC ≈ vD
````

````
true
````

## Pregunta 093

Considere dos matrices `mA` y `mB` de tamaños `8x3` y `2x2`. Encuentre filas de `mA` que contengan elementos de cada fila de `mB` independientemente del orden de los elementos en `mB`. (★★★)

La forma en que interpreto la pregunta son las filas en `ma` que contienen al menos 1 elemento de cada fila de 'mB`.

````julia
mA = rand(0:4, 8, 3);
mB = rand(0:4, 2, 2);
mC = [any(vA .== vB') for vB in eachrow(mB), vA in eachrow(mA)]; #<! General solution, will work for any size of `mA` and `mB`
vD = [all(vC) for vC in eachcol(mC)]
````

````
8-element Vector{Bool}:
 0
 1
 1
 1
 0
 0
 1
 1
````

Para tener una solución sin la matriz intermedia `mc`

````julia
function Iterate2(iA; iterState = missing)
    if(ismissing(iterState))
        valA, iterState = iterate(iA);
    else
        valA, iterState = iterate(iA, iterState);
    end
    valB, iterState = iterate(iA, iterState);
    return (valA, valB), iterState
end

tT = (any(vA .== vB') for vB in eachrow(mB), vA in eachrow(mA));

iterState = missing;

vE = zeros(Bool, size(mA, 1));

for ii = 1:length(vD)
    global iterState;
    (valA, valB), iterState = Iterate2(tT; iterState = iterState);
    vE[ii] = valA && valB;
end

vD == vE
````

````
true
````

## Pregunta 094

Teniendo en cuenta una matriz `10x3`, extraiga filas con valores desiguales. (★★★)

````julia
mA = rand(1:3, 10, 3);
vD = [maximum(vA) != minimum(vA) for vA in eachrow(mA)]
````

````
10-element Vector{Bool}:
 1
 0
 1
 1
 1
 1
 1
 1
 1
 1
````

## Pregunta 095

Convierta un vector de enteros en una representación binaria de matriz. (★★★)
Convert a vector of ints into a matrix binary representation. (★★★)

````julia
vA = rand(UInt8, 10);
mB = zeros(Bool, length(vA), 8);

# Ver https://discourse.julialang.org/t/26663
for ii in 1:length(vA)
    vS = bitstring(vA[ii]);
    for jj in 1:size(mB, 2)
        mB[ii, jj] = vS[jj] == '1';
    end
end

mB
````

````
10×8 Matrix{Bool}:
 0  0  1  0  1  1  1  1
 1  1  0  1  1  1  0  0
 0  0  0  0  1  0  1  0
 1  1  1  0  0  1  0  1
 0  1  0  1  0  1  0  1
 0  0  0  1  0  1  1  1
 1  0  0  0  1  0  1  0
 1  1  0  1  1  1  0  0
 0  0  1  1  1  1  0  0
 1  0  0  0  0  1  0  0
````

Por [Tomer Arnon](https://github.com/tomerarnon):

````julia
mB = reverse!(reduce(hcat, digits.(vA, base = 2, pad = 8))', dims = 2);
````

## Pregunta 096

Dada una matriz bidimensional, extraiga las filas únicas. (★★★)

````julia
mA = UInt8.(rand(1:3, 10, 3));

vS = [reduce(*, bitstring(valA) for valA in vA) for vA in eachrow(mA)]; #<! Funciona para todo arreglo!
vU = unique(vS);
vI = [findfirst(valU .== vS) for valU in vU];
````

Una forma alternativa:

````julia
vB = indexin(vU, vS);
vB == vI
````

````
true
````

## Pregunta 097

Considerando 2 vectores `vA` y `vB`, escriba el equivalente de Einsum (usando `Einsum.jl`) de la funciónes `inner`, `outer`, `sum` y `mul`. (★★★)

````julia
vA = rand(5);
vB = rand(5);
````

Producto interno

````julia
@tullio tullioVal = vA[ii] * vB[ii];
tullioVal ≈ dot(vA, vB) #<! Inner product
````

````
true
````

Producto exterior

````julia
@tullio mTullio[ii, jj] := vA[ii] * vB[jj]; #<! Outer product
mTullio ≈ vA * vB'
````

````
true
````

Sums

````julia
@tullio tullioVal = vA[ii];
tullioVal ≈ sum(vA) #<! Sum
````

````
true
````

Multiplicación

````julia
@tullio vTullio[ii] := vA[ii] * vB[ii];
vTullio ≈ vA .* vB #<! Multiplication
````

````
true
````

## Pregunta 098

Teniendo en cuenta una ruta descrita por dos vectores `vX` y `vY`, muestréelo utilizando muestras equidistantes. (★★★)

La forma en que interpreté la pregunta es crear sub segmentos de la misma longitud.

````julia
numPts      = 100;
numSegments = 1000;

vX = sort(10 * rand(numPts));
vY = sort(10 * rand(numPts));

vR = cumsum(hypot.(diff(vX), diff(vY)));
pushfirst!(vR, 0.0);
vRSegment = LinRange(0.0, vR[end], numSegments);

struct LinearInterpolator1D{T <: Number} <: AbstractArray{T, 1}
    vX::Vector{T};
    vY::Vector{T};

    function LinearInterpolator1D(vX::Vector{T}, vY::Vector{T}) where {T <: Number}
        length(vX) == length(vX) || throw(ArgumentError("Input vectors must have the same length"));
        new{T}(vX, vY);
    end
end

function Base.size(vA::LinearInterpolator1D)
    size(vA.vX);
end
function Base.getindex(vA::LinearInterpolator1D, ii::Number)
    if (ii >= vA.vX[end])
        return vA.vY[end];
    end
    if (ii <= vA.vX[1])
        return vA.vY[1];
    end

    rightIdx = findfirst(vA.vX .>= ii);
    leftIdx = rightIdx - 1;

    tt = (ii - vA.vX[leftIdx]) / (vA.vX[rightIdx] - vA.vX[leftIdx]);

    return ((1 - tt) * vA.vY[leftIdx]) + (tt * vA.vY[rightIdx]);

end
function Base.setindex!(vA::LinearInterpolator1D, valX, valY, ii::Int, jj::Int)
    setindex!(sLinInterp.vX, valX, ii);
    setindex!(sLinInterp.vY, valY, ii);
end

vXInt = LinearInterpolator1D(vR, vX);
vYInt = LinearInterpolator1D(vR, vY);

vXSegment = [vXInt[intIdx] for intIdx in vRSegment];
vYSegment = [vYInt[intIdx] for intIdx in vRSegment];

hP = lineplot(vX, vY, canvas = DotCanvas, name = "Samples");
lineplot!(hP, vXSegment, vYSegment, name = "Interpolated");
hP
````

````
      ┌────────────────────────────────────────┐             
   10 │                                     ..:│ Samples     
      │                                 ...''  │ Interpolated
      │                              .:''      │             
      │                             .:         │             
      │                            .:          │             
      │                        .:'''           │             
      │                       :'               │             
      │                    ..:'                │             
      │                  :''                   │             
      │              ....:                     │             
      │            ..:                         │             
      │        :''''                           │             
      │     .:''                               │             
      │   .:'                                  │             
    0 │..:'                                    │             
      └────────────────────────────────────────┘             
       0                                     10              
````

**Observación**: Para ser matemáticamente preciso, la resolución de `vRSegment` debe ser lo suficientemente alta como para ser un factor entero de cada segmento.
Se puede hacer si la resolución es `1 / (Prod (vR))` que es fácilmente intractable con `Float64`. Así que esta es una aproximación lo suficientemente buena.

## Pregunta 099

Dado un entero `n` y una matriz 2D `mA`, encuentre las filas que pueden interpretarse como extraídas de una distribución multinomial con `n` (filas que solo contienen enteros y que suma a `n`). (★★★)

````julia
mA = rand([0, 0.5, 1, 2, 3], 15, 3);
sumVal = 4;
vI = [all(vA .== round.(vA)) && sum(vA) == sumVal for vA in eachrow(mA)];
````

## Pregunta 100

Calcule los intervalos de confianza `95%` para la media de una matriz 1D 'vA'. A saber, vuelva a muestrear los elementos de una matriz con tiempos de reemplazo `n`, calcule la media de cada muestra y luego calcule los percentiles sobre los medios. (★★★)

````julia
numTrials   = 10000;
numSamples  = 1000;
μ           = 0.5;

vA = μ .+ randn(numSamples);
tM = (mean(vA[rand(1:numSamples, numSamples)]) for _ in 1:numTrials);
quantile(tM, [0.025, 0.975])
````

````
2-element Vector{Float64}:
 0.4620914889349693
 0.5830619321705541
````

---

*This page was generated using [Literate.jl](https://github.com/fredrikekre/Literate.jl).*

