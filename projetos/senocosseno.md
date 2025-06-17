# Cena 1

```python
#*********************************************************************** 
%%manim -ql -v WARNING Seno_Cosseno0
#*********************************************************************** 
class Seno_Cosseno0(Scene):
  def construct(self):
    #*********************************************************************** Texto Introdutório
    # POWER VISUALS APRESENTA
    # Funcões: Seno e Cosseno
    #**********************************************************************
    text0 = Tex('\\textsc{POWER VISUALS}').shift(UP).set_width(8).set_color_by_gradient(YELLOW, BLUE)
    text00 = Tex('\\textit{ Apresenta}').shift(DOWN).set_width(3)

    text1 = Tex('\\textsc{FUNÇÕES}').shift(UP).set_width(4)
    text2 = Tex('\\textit{Seno e Cosseno}').set_width(8).set_color(YELLOW).set_opacity(1)

    #***********************************************************************
    # De onde elas Veêm ?
    #***********************************************************************
    text3 = Tex('\\textrm{De onde elas Vêm ?}').set_width(8)


    #*********************************************************************** Ferramentas Base
    # Plano Cartesiano e Círunferência Unitária

    axes = Axes(
        x_range = [-2,2,0.5],
        y_range = [-2,2,0.5],
        x_length = 4,
        y_length = 4
    )
    axes.to_edge(LEFT, buff = 1.5)

    circle = Circle(radius = 1, stroke_color = GREEN_E, stroke_width = 8)
    circle.to_edge(RIGHT, buff = 1.5)
    #***********************************************************************


    ######################################################################## Texto Introdutório
    # Funcões: Seno e Cosseno
    ########################################################################
    self.wait(0.5)
    self.play(Write(text0))
    self.wait(0.5)

    self.play(Write(text00))


    self.play(Unwrite(text0))
    self.play(Unwrite(text00))

    self.play(Write(text1))

    self.play(ReplacementTransform(text1,text2), run_time = 2)

    self.wait()

    self.play(Unwrite(text2))

    self.wait()     ############### estou aqui

    #######################################################################
    # De onde elas Veêm?
    ########################################################################
    self.play(Write(text3), run_time = 0.8)
    self.play(FadeOut(text3), run_time = 0.8)

    ########################################################################  Ferramentas Base
    # Plano Cartesiano e Círunferência Unitária
    ########################################################################

    plano = Tex('\\textit{Plano}').next_to(axes, DOWN, buff = 0.5)
    circun = Tex('\\textit{Circunferência}').next_to(circle, DOWN, buff = 0.2)
    unit = Tex('\\textit{unitária}').next_to(circun, DOWN, buff = 0.5)


    self.play( Write(axes), Create(circle) , run_time = 4 )
    self.play(Write(plano),LaggedStart( Write(circun), Write(unit),  lag_ratio = 0.5))

    self.play(Unwrite(plano), Unwrite(circun),Unwrite(unit))
    self.wait(1)

    #***********************************************************************
    def center():
      return np.array([0,0,0])
    #***********************************************************************
    self.wait(2)
    self.play(circle.animate.move_to( center() ), axes.animate.move_to( center() ), run_time = 2)
    self.play(circle.animate.set_width(4), axes.animate.set_width(8), run_time = 2)

    #********************* Escala de Unidade
    Unidade0H = MathTex('1').next_to(axes.c2p(1,0), UP, buff = 0.2)
    Unidade1H = MathTex('0').next_to(axes.c2p(0,0), UP, buff = 0.2).shift(0.2*LEFT)
    Unidade2H = MathTex('-1').next_to(axes.c2p(-1,0), UP, buff = 0.2)

    Unidade0V = MathTex('1').next_to(axes.c2p(0, 1), LEFT, buff = 0.2)

    Unidade2V = MathTex('-1').next_to(axes.c2p(0, -1), LEFT, buff = 0.2)
    grupo_numéricoH = VGroup(Unidade0H, Unidade1H,Unidade2H)
    grupo_numéricoV = VGroup(Unidade0V, Unidade2V)
    #*********************

    #********************** Nome dos eixos
    texto_h = Tex('\\textit{Horizontal}').next_to(axes.c2p(1.7,0), DOWN, buff= 0.5)
    texto_v = Tex('\\textit{Vertical}'  ).rotate(angle = PI/2).next_to(axes.c2p(0,1.4), LEFT, buff= 0.5)
    #**************************************

    self.play( circle.animate.set_stroke(opacity = 0.4), axes.animate.set_stroke(opacity = 0.4))
    self.play( Write(grupo_numéricoH))
    self.play( Write(grupo_numéricoV))
    self.play(Write(texto_h), Write(texto_v), run_time = 2.5)

    self.play( Unwrite(grupo_numéricoH), Unwrite(grupo_numéricoV), Unwrite(texto_v), Unwrite(texto_h), run_time = 1.5 )
    self.play( circle.animate.set_stroke(opacity = 1), axes.animate.set_stroke(opacity = 1))


    self.wait()
    ########################################################################
```

----------------------------

# Cena 2

    %%manim -qm -v WARNING Seno_Cosseno1
    
    class Seno_Cosseno1(Scene):
      def construct(self):

    self.camera.background_color =  BLACK

    axes = Axes(
        x_range = [-2,2,0.5],
        y_range = [-2,2,0.5],
        x_length = 4,
        y_length = 4,
        stroke_width  = 10

    ).set_width(8)

    circle = Circle(radius = 1, stroke_color = GREEN, stroke_width = 8, ).set_width(4)
    self.add(circle, axes)



    ###################################################################################################################################### Partícula dá um giro
    #********************************************************************************
    t = ValueTracker(0)
    t1 = ValueTracker(0.8)
    particula = always_redraw( lambda:  Dot(axes.c2p(np.cos( t.get_value() ), np.sin( t.get_value() ) ), color = RED).set_width(t1.get_value()) )
    #********************************************************************************

    self.play( FadeIn( particula ), run_time =1.5)
    self.play( t1.animate.set_value(0.25), run_time = 2)

    texto_ponto = Tex('(1,0)').next_to(particula, RIGHT+DOWN, buff = 0.2).scale(0.8)
    self.play(Write(texto_ponto))
    self.wait()
    self.play(Unwrite(texto_ponto))

    self.play( t.animate.set_value(2*PI), run_time = 4)   # PARTÍCULA DÁ UM GIRO DE 360 GRAUS

    self.wait()
    ######################################################################################################################################




    ####################################################################################################################################### Coloca Coordenadas da PARTÍCULA
    #********************************************************************************
    t.set_value(0)
    #********************************************************************************

    self.play(t.animate.set_value(PI/3.5), run_time = 4)  # PARTÍCULA PERCORRE UM ARCO PEQUENO

    #******************************************************************************** CRIA LINHAS H e V
    opacidade_a, opacidade_b = 1, 1
    lineH = always_redraw( lambda: axes.get_horizontal_line( particula.get_center() , line_func = Line).set_opacity( opacidade_b )  )
    lineV = always_redraw( lambda: axes.get_vertical_line  ( particula.get_center() , line_func = Line).set_opacity( opacidade_a )  )
    #********************************************************************************

    self.play( circle.animate.set_stroke( opacity = 0.3),axes.animate.set_opacity(0.3))
    self.play( Create(lineH),Create(lineV), run_time =2 ) # ESCREVE LINHAS H e V


    #******************************************************************************** CRIA COORDENADAS
    a = always_redraw( lambda:  Text('a').next_to(lineV, DOWN, buff = 0.5).set_opacity( opacidade_a )  )
    b = always_redraw( lambda:  Text('b').next_to(lineH, LEFT, buff = 0.5).set_opacity( opacidade_b )  )
    #********************************************************************************
    self.wait(4)
    self.play(Write(a),Write(b))
    #######################################################################################################################################


    ####################################################################################################################################### Enfatiza coordenada 'A'
    #********************************************************************************
    t.set_value(0)
    opacidade_b = 0.3
    dota = always_redraw( lambda: Dot(axes.c2p(np.cos(t.get_value()),0)))

    #********************************************************************************
    self.wait(3)

    #********************* Escala de Unidade
    Unidade0H = MathTex('1').next_to(axes.c2p(1,0), UP, buff = 0.2)
    Unidade1H = MathTex('0').next_to(axes.c2p(0,0), UP, buff = 0.2).shift(0.2*LEFT)
    Unidade2H = MathTex('-1').next_to(axes.c2p(-1,0), UP, buff = 0.2)

    Unidade0V = MathTex('1').next_to(axes.c2p(0, 1), LEFT, buff = 0.2)
    Unidade1V = MathTex('0').next_to(axes.c2p(0,0), UP, buff = 0.2).shift(0.2*LEFT)
    Unidade2V = MathTex('-1').next_to(axes.c2p(0, -1), LEFT, buff = 0.2)
    grupo_numéricoH = VGroup(Unidade0H, Unidade1H, Unidade2H)
    grupo_numéricoV = VGroup(Unidade0V, Unidade2V)
    #*********************
    self.play( Write(grupo_numéricoH))
    self.play(FadeIn(dota))
    self.play(t.animate.set_value(2*PI), run_time = 4)
    self.play( Unwrite(grupo_numéricoH), FadeOut(dota))
    #######################################################################################################################################



    ####################################################################################################################################### Enfatiza a coordenada 'B'
    #********************************************************************************
    t.set_value(0)
    opacidade_b = 1
    opacidade_a = 0.3
    dotb = always_redraw(lambda: Dot(axes.c2p(0,np.sin(t.get_value()))))
    #********************************************************************************

    self.play( Write( grupo_numéricoV), Write(Unidade1V))
    self.play(FadeIn(dotb))
    self.play(t.animate.set_value(2*PI), run_time = 9)
    self.play( Unwrite(grupo_numéricoV), Unwrite(Unidade1V), FadeOut(dotb), run_time = 2)
    #######################################################################################################################################


    ####################################################################################################################################### MOSTRAR COORDENADAS COMO FUNÇÕES a(s) E b(s)
    #******************************************************************************** # TRAÇO PERCORRIDO PELA PARTÍCULA
    arco = always_redraw( lambda: axes.plot_parametric_curve( lambda t: np.array(
                                                         [np.cos(t),np.sin(t)]
                                                         ),t_range = [0, t.get_value() ], color = RED ) )
    #********************************************************************************
    self.wait(4)
    self.add(arco) # ADICIONA O TRAÇO VERMELHO NA TELA

    #********************************************************************************
    opacidade_a = 1
    t.set_value(0)
    #********************************************************************************

    self.play(t.animate.set_value(PI/3.5), run_time = 6) # CRIA UM PEQUENO TRAÇO

    #********************************************************************************
    s = Text('s', color = RED).next_to( particula,2* RIGHT + 0.7*DOWN, buff = 0.5 )
    #********************************************************************************

    self.play( Write(s), run_time = 3 )  # DENOMINA O COMPRIMENTO DO TRAÇO COMO S

    #********************************************************************************  cria coordenadas a(s) e b(s)
    func_a = always_redraw(lambda:  MathTex('a(s)' ).next_to(lineV, DOWN, buff = 0.5).set_opacity( opacidade_a ) )
    func_b = always_redraw(lambda:  MathTex('b(s)').next_to(lineH, LEFT, buff = 0.5).set_opacity( opacidade_b ) )
    #********************************************************************************

    self.play(FadeOut(a), FadeOut(b), FadeIn(func_a), FadeIn(func_b), run_time = 5 )  # coloca na tela coordenadas a(s) e b(s)

    self.wait(3)
    self.play(Unwrite(func_a), Unwrite(func_b), run_time = 4)
    self.wait()
    self.play(FadeOut(s), FadeOut(arco), FadeOut(particula), FadeOut(lineH), FadeOut(lineV), run_time = 3)

    #######################################################################################################################################

------------------------------------------------------------------------------------------

# Cena 3

    %%manim -qh -v WARNING Seno_Cosseno2
    
    class Seno_Cosseno2(Scene):
      def construct(self):

    self.camera.background_color =  BLACK

    axes = Axes(
        x_range = [-2,2,0.5],
        y_range = [-2,2,0.5],
        x_length = 4,
        y_length = 4,
        stroke_width  = 10

    ).set_width(8)

    circle = Circle(radius = 1, stroke_color = GREEN, stroke_width = 8, ).set_width(4)
    t =ValueTracker(0)
    tn = ValueTracker(0)


    # IDÉIA: ANTES DE INTRODUZIR AS EQUAÇÕES COLOCAR UM PLANO OPACO NA CENA E DAÍ ENFATIZAR AS EQUAÇÕES AO INVÉS DE RETIRAR OS ELEMENTOS

    ####################################################################################################################################### coloca elementos na cena(idéia)
    self.add(circle.set_stroke(opacity = 0.5), axes.set_opacity(0.3))  # adiciona elementos base na cena translúcidos

    #********************************************************************************CRIA PARTICULA
    particula = always_redraw( lambda:  Dot(axes.c2p(np.cos( t.get_value() ), np.sin( t.get_value() ) ), color = RED).set_width(0.25) )

    arco = always_redraw( lambda: axes.plot_parametric_curve( lambda t: np.array(
                                                         [np.cos(t),np.sin(t)]
                                                         ),t_range = [tn.get_value(), t.get_value() ], color = RED ) )  # CRIA ARCO
    #********************************************************************************

    #############################################################
    self.play( FadeIn(particula), run_time = 2 )  # COLOCA PARTÍCULA NA CENA
    self.add(arco)                  # COLOCA TRAÇO NA CENA
    #############################################################

    ########################################################################################################################### Equações de comprimento de arco



    #********************************************** retangulo translúcido    #############
    retângulo = Rectangle(width=20, height=10, fill_opacity = 0.8, color = BLACK)
    self.play(FadeIn(retângulo), run_time = 3)
    self.wait(3)
    #*********************************************** cria equações de comprimentos de arco
    equacao1 = MathTex('S = 2 \pi R').set_width(6).scale(0.7).shift(1.5*LEFT + UP)
    equacao2 = MathTex('S = 2 \pi').set_width(6).scale(0.6).shift(1.5*LEFT+UP)
    #***********************************************

    self.play(Write(equacao1), run_time = 2)  # escreve equação de um arco genérico
    self.wait(2)
    self.play(Transform(equacao1,equacao2), run_time = 3) # tranforma equação de arco duma circunferência genérica em uma unitátria
    self.wait(2)
    self.play( Unwrite (equacao1), run_time = 3 )

    ###########################################################################################################################

    ########################################################################################################################### Apresenta o radiano
    self.wait()
    #********************************************************************************
    radian = Tex('\\textit{Radianos}').scale(3)
    #********************************************************************************
    self.play(Write(radian))     # escreve a unidade radianos
    self.wait()
    self.play(Unwrite(radian))
    ##########################################################################################################################

    self.play(FadeOut(retângulo))
    ####################################################################################################################################### Apresentar coordenadas a(s) e b(s)

    #********************************************************************************
    opacidade_a = 1
    t.set_value(0)
    #********************************************************************************

    #********************************************************************************
    lineH = always_redraw( lambda: axes.get_horizontal_line( particula.get_center() , line_func = Line) )
    lineV = always_redraw( lambda: axes.get_vertical_line( particula.get_center() , line_func = Line) )
    #********************************************************************************

    #############################################################
    self.play( Create(lineH), Create(lineV) )
    #############################################################

    #********************************************************************************
    func_a = always_redraw(lambda:  MathTex('a(s)').next_to(lineV, DOWN, buff = 0.5) )
    func_b = always_redraw(lambda:  MathTex('b(s)').next_to(lineH, LEFT, buff = 0.5) )
    #********************************************************************************

    self.play( FadeIn(func_a), FadeIn(func_b), run_time = 3 ) # coloca coordenadas a(s) e b(s)

    ######################################################################################################################################

    ###################################################################################################################################### DAR EXEMPLO DO COMPRIMENTO EM UNIDADE DE RADIANOS
    #******************************************************************************** EStOU AQUI
    s = Text('s', color = RED).next_to( particula,1.8* RIGHT + 1.5*UP, buff = 0.5 )

    s0 = Text('s = ').next_to( particula,1.8*RIGHT + 1.5*UP, buff = 0.5 )

    s1 = MathTex('\\frac{\pi}{2}').next_to(s0, RIGHT, buff = 0.2)
    s2 = MathTex('\pi').next_to(s0, RIGHT, buff = 0.2)
    s3 = MathTex('3\\frac{\pi}{2}').next_to(s0, RIGHT, buff = 0.2)
    s4 = MathTex('2\pi}').next_to(s0, RIGHT, buff = 0.2)
    radian0 = Tex('\\textit{Radianos}')
    #********************************************************************************
    self.play( t.animate.set_value(PI/2))  # cria traço de 1/4 de circunferência
    self.play( Write(s0) )  # escreve letra do traço
    self.play( Write(s1))   # escreve o comprimento do traço de PI/2 RADIANOS


    self.play( Write(radian0.next_to(s1, RIGHT,buff = 0.3).scale(0.9))  ) # escreve unidade radianos
    self.play( Unwrite(radian0))


    self.play( t.animate.set_value(PI),ReplacementTransform(s1,s2) , run_time = 2.5)        # cria traço de 2/4 de circunferência
    self.play( t.animate.set_value(3*(PI/2)),ReplacementTransform(s2,s3) , run_time = 3)        # cria traço de 3/4 de circunferência
    self.play( t.animate.set_value(2*PI),ReplacementTransform(s3,s4) , run_time = 3)        # cria traço de 4/4 de circunferência


    self.wait()
    t.set_value(0)
    self.play( FadeOut(s4), FadeOut(particula), FadeOut(lineH), FadeOut(lineV), FadeOut(func_a), FadeOut(func_b) )




    #********************************************************************************
    particulan = always_redraw( lambda:  Dot(axes.c2p(np.cos( tn.get_value() ), np.sin( tn.get_value() ) ), color = RED).set_width(0.25) )
    s1 = MathTex('-\\frac{\pi}{2}').next_to(s0, RIGHT, buff = 0.2)
    s2 = MathTex('-\pi').next_to(s0, RIGHT, buff = 0.2)
    s3 = MathTex('-3\\frac{\pi}{2}').next_to(s0, RIGHT, buff = 0.2)
    s4 = MathTex('-2\pi}').next_to(s0, RIGHT, buff = 0.2)
    #********************************************************************************
    self.play(FadeIn(particulan))
    self.play( tn.animate.set_value(-PI/2), run_time = 3)  # cria traço de 1/4 de circunferência
    self.play( Write(s1))   # escreve o comprimento do traço de PI/2 RADIANOS
    self.play( tn.animate.set_value(-PI),ReplacementTransform(s1,s2) , run_time = 3)        # cria traço de 2/4 de circunferência
    self.play( tn.animate.set_value(-3*(PI/2)),ReplacementTransform(s2,s3) , run_time = 3)        # cria traço de 3/4 de circunferência
    self.play( tn.animate.set_value(-2*PI),ReplacementTransform(s3,s4) , run_time = 3)        # cria traço de 4/4 de circunferência

    tn.set_value(0)
    self.wait()
    self.play( FadeOut(s4), FadeOut(s0),FadeIn(s) )

    self.wait(2)

    self.play(FadeIn(lineH),FadeIn(lineV), FadeIn(func_a), FadeIn(func_b), FadeIn(particula),FadeOut(particulan))
    self.play( t.animate.set_value(PI/3.5), run_time = 9)

    #***************************************************************
    line1 = always_redraw( lambda: Line(start = axes.c2p(0,0), end = particula.get_center() ) )
    #***************************************************************
    self.play(Create(line1), run_time = 3)
    self.play( FadeOut(lineH), FadeOut(lineV), run_time = 5)
    self.wait()

    ######################################################################################################################################  preparando escrita  da função cosseno
    #*******************************************************
    func_a1 = func_a.copy().to_edge(LEFT + UP, buff = 1.5 )
    #*******************************************************
    self.play( ReplacementTransform( func_a, func_a1 ) )

    #*******************************************************
    igual = MathTex('=').next_to(func_a1, RIGHT, buff = 0.5)
    func_cosseno = MathTex('cos(s)').next_to(igual, RIGHT, buff = 0.5)
    #*******************************************************

    self.play(Create(igual))
    self.play(Write(func_cosseno))
    ###############################################################################

    ####################################################################################################################################### preparando escrita da função seno
    #*******************************************************
    func_b1 = func_b.copy().next_to(func_a1, DOWN,  buff = 0.5 )
    #*******************************************************
    self.play( ReplacementTransform( func_b, func_b1 ) )

    #*******************************************************
    igual2 = MathTex('=').next_to(func_b1, RIGHT, buff = 0.5)
    func_seno = MathTex('sen(s)').next_to(igual2, RIGHT, buff = 0.5)
    #*******************************************************
    self.play(Create(igual2))
    self.play(Write(func_seno), run_time = 2)
    self.wait(10)
    self.play(FadeOut(func_b1), FadeOut(igual2), FadeOut( func_seno ), run_time = 4)
    self.wait(3)
    ###############################################################################


    ####################################################################################################################### Colocar plano no lado direito da tela e diminuir seu tamanho
    self.play(t.animate.set_value(PI*2), run_time = 4)

    #*******************************************************
    grupo = VGroup( axes, circle, s ,particula , arco)
    #*******************************************************

    self.play( grupo.animate.shift(4*RIGHT + UP).set_width(3), run_time = 4)
    #######################################################################################################################'''

----------------------------------------------------------------------------------------

# Cena 4

    %%manim -qh -v WARNING mostrar_coseno
    class mostrar_coseno(Scene):
        def construct(self):
  

        #*********************************************************************************************************************************************************
        axes = Axes(
        x_range = [-2,2,0.5],
        y_range = [-2,2,0.5],
        x_length = 4,
        y_length = 4,
        stroke_width  = 10

         ).set_width(8).set_opacity(0.3) # CRIA EIXOS PARA O CÍRCULO

        circle = Circle(radius = 1, stroke_color = GREEN, stroke_width = 8, ).set_width(4).set_stroke(opacity = 0.5) # cria írculo
        t =ValueTracker(2*PI)  # cria variável

        particula = Dot(axes.c2p(np.cos( t.get_value() ), np.sin( t.get_value() ) ), color = RED).set_width(0.25)  # CRIA PARTICULA

        arco = always_redraw( lambda: axes.plot_parametric_curve( lambda t: np.array(
                                                         [np.cos(t),np.sin(t)]
                                                         ),t_range = [0, t.get_value() ], color = RED ) )  # CRIA ARCO

        linha_auxiliar0 = Line( start = axes.c2p(-1,0), end = axes.c2p(1,0), color =  YELLOW, stroke_width = 8).set_opacity(0)
        grupo = VGroup( axes, circle, arco,linha_auxiliar0)  # grupo dos elementos base

        #*******************************************************  texto função cosseno
        func_a = always_redraw(lambda:  MathTex('a(s)').to_edge(LEFT + UP, buff = 1.5 ))
        igual = MathTex('=').next_to(func_a, RIGHT, buff = 0.5)
        func_cosseno = MathTex('cos(s)').next_to(igual, RIGHT, buff = 0.5)
        #*******************************************************

        #**********************************************************************************************************************************************************
        #**********************************************************************************************************************
        axes1 = Axes(x_range = [-8,8,PI/2], y_range = [-2,2,1], x_length = 10,y_length = 5).to_edge(LEFT + DOWN,buff = 0.2)# eixos do cos e sen
        axes2 =Axes( y_range = [-8,8,1], y_length = 8) # eixos auxiliares
        line_arco = Line( start = axes2.c2p(0,0), end = axes2.c2p(0,2*PI), color =  RED, stroke_width = 8) # Segmento Vertical
        line_axes = Line(start = axes1.c2p(2*PI,0),  end = axes1.c2p(0,0), color =  RED, stroke_width = 8) # Segmento horizontal
        line_axes_negativo = Line(start = axes1.c2p(0,0),  end = axes1.c2p(-2*PI,0), color =  RED, stroke_width = 8) # Segmento horizontal

        #********************* escala radianos positivos e negativos
        tnum = 0.8
        n0 = MathTex('0').next_to( axes1.c2p(0,0),UP + LEFT, buff = 0.2 ).scale(tnum)
        n1 = MathTex('\\frac{\\pi}{2}').next_to(axes1.c2p(PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        n2 = MathTex('\\pi').next_to(axes1.c2p(PI,0), UP, buff = 0.2 ).scale(tnum)
        n3 = MathTex('3\\frac{\\pi}{2}').next_to(axes1.c2p(3*PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        n4 = MathTex('2\\pi').next_to(axes1.c2p(2*PI,0), UP , buff = 0.2 ).scale(tnum)
        grupo_radianos = VGroup(n0, n1, n2, n3, n4)

        N1 = MathTex('-\\frac{\\pi}{2}').next_to(axes1.c2p(-PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        N2 = MathTex('-\\pi').next_to(axes1.c2p(-PI,0), UP, buff = 0.2 ).scale(tnum)
        N3 = MathTex('-3\\frac{\\pi}{2}').next_to(axes1.c2p(-3*PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        N4 = MathTex('-2\\pi').next_to(axes1.c2p(-2*PI,0), UP , buff = 0.2 ).scale(tnum)
        grupo_radianos_n = VGroup( N1, N2, N3, N4)
        #*********************

        #********************* Escala de Unidade
        Unidade0 = MathTex('1').next_to(axes1.c2p(0, 1), LEFT, buff = 0.2)
        Unidade1 = MathTex('-1').next_to(axes1.c2p(0, -1), LEFT, buff = 0.2)
        grupo_numérico = VGroup(Unidade0, Unidade1)
        #*********************


        #************************ ELEMENTOS DO TRAÇO DO COSSENO

        theta_p = ValueTracker(0)
        theta_n = ValueTracker(0)
        traço_cosseno = always_redraw(lambda: axes1.plot(lambda x: np.cos(x), x_range = [theta_n.get_value(),theta_p.get_value()], color = YELLOW) )
        dot_cosseno = always_redraw(lambda: Dot(axes1.c2p(theta_p.get_value(), np.cos(theta_p.get_value()))) )
        dot_cosseno_n = always_redraw(lambda: Dot(axes1.c2p(theta_n.get_value(), np.cos(theta_n.get_value()))) )
        linha_h_traço = always_redraw( lambda: axes1.get_horizontal_line( dot_cosseno.get_center() , line_func = Line) )
        linha_v_traço = always_redraw( lambda: axes1.get_vertical_line( dot_cosseno.get_center() , line_func = Line) )
        linha_auxiliar1 = Line( start = axes1.c2p(0,-1), end = axes1.c2p(0, 1), color = YELLOW, stroke_width = 8 )

        #******************************************************************************************************* RÓTULOS DA FUNÇÃO COSSENO
        rótulo_v = MathTex('a').next_to(axes1, UP, buff = -0.4).shift(0.6*LEFT).set_color(YELLOW).scale(1.5)
        rótulo_h =  MathTex('s').next_to(axes1, RIGHT, buff = -0.4).shift(0.6*DOWN).set_color(RED).scale(1.5)
        #*******************************************************************************************************

        partícula_h = always_redraw(lambda: Dot(axes1.c2p(theta_p.get_value(),0)).set_color(RED).scale(1.3) )
        partícula_a = always_redraw(lambda: Dot(axes1.c2p(0, np.cos(theta_p.get_value()))).set_color(YELLOW).scale(1.3) )

        partícula_hn = always_redraw(lambda: Dot(axes1.c2p(theta_n.get_value(),0)).set_color(RED).scale(1.3) )
        partícula_an = always_redraw(lambda: Dot(axes1.c2p(0, np.cos(theta_n.get_value()))).set_color(YELLOW).scale(1.3) )


        #********************************************************************************************************
        retângulo = RoundedRectangle(corner_radius = 0.1,stroke_color = WHITE, stroke_width = 3,
                               height = 0.5, width  = 2).shift(UP+RIGHT*4)

        grupo.shift(4*RIGHT + UP).set_width(3)
        #****************************************************************************************************************

        ####################################################################################################################################### COMEÇO DO VÍDEO
        self.add(grupo)
        self.add(func_a)
        self.add(igual)
        self.add(func_cosseno)

        ######################################################### preparando elementos para plotar o gráfico positivo
        self.wait()
        self.play( Write (axes1) )
        self.play( Write (rótulo_h), Write (rótulo_v) )
        self.play( ReplacementTransform (arco,line_arco))
        self.play( ReplacementTransform (line_arco,line_axes) )
        self.play( FadeOut (line_axes), Write(grupo_radianos) )
        self.play( Create (retângulo) )
        self.play( linha_auxiliar0.animate.set_opacity(1) )
        self.play( FadeOut (retângulo), ReplacementTransform( linha_auxiliar0, linha_auxiliar1) )
        self.play( FadeOut (linha_auxiliar1))
        self.play( Write (grupo_numérico) )
        self.add ( dot_cosseno)
        self.play( FadeIn(traço_cosseno), FadeIn(partícula_h), FadeIn(partícula_a) )

        #********************************************************************************
        lineHp = always_redraw( lambda: axes1.get_horizontal_line( dot_cosseno.get_center() , line_func = Line) )
        lineVp = always_redraw( lambda: axes1.get_vertical_line( dot_cosseno.get_center() , line_func = Line) )
        #********************************************************************************
        self.add(lineHp, lineVp)

        ############################################################################################################

        ############################################################## Cria gráfico cosseno parte positiva
        self.play( theta_p.animate.set_value(PI/2), run_time = 2 )
        self.play( theta_p.animate.set_value(PI), run_time = 2)
        self.play( theta_p.animate.set_value( 3*(PI/2)), run_time = 2)
        self.play( theta_p.animate.set_value(2*PI) , run_time = 2)
        self.play( FadeOut( lineHp, lineVp, dot_cosseno))
        #######################################################################################################

        #*******************************************************
        traço_cópia = traço_cosseno.copy()
        #*******************************************************

        self.play( FadeOut(traço_cosseno),FadeOut(partícula_a),FadeOut(partícula_h))

        #*******************************************************
        theta_p.set_value(0)
        #*******************************************************

        ######################################################## preparando elementos para plotar o gráfico negativo
        self.play(FadeIn(arco))
        self.play( ReplacementTransform (arco,line_arco))
        self.play( ReplacementTransform (line_arco,line_axes_negativo) )
        self.play( FadeOut( line_axes_negativo) )
        self.play(  Write (grupo_radianos_n))
        self.add(dot_cosseno_n)

        #********************************************************************************
        lineHn = always_redraw( lambda: axes1.get_horizontal_line( dot_cosseno_n.get_center() , line_func = Line) )
        lineVn = always_redraw( lambda: axes1.get_vertical_line( dot_cosseno_n.get_center() , line_func = Line) )
        #********************************************************************************
        self.add(lineHn, lineVn)

        ########################################################

        ############################################################## Cria gráfico cosseno parte negativa
        self.add ( traço_cosseno )
        self.add ( partícula_an, partícula_hn)
        self.play( theta_n.animate.set_value(-2*PI), run_time = 4)
        self.play( FadeOut( lineHn, lineVn, dot_cosseno_n))
        #############################################################

        ############################################################# Finaliza gráfico Cosseno

        self.play(FadeIn (traço_cópia), FadeOut(partícula_an, partícula_hn), run_time = 3)


        ############################################################################################################################################################################
        #self.add( axes1, line_arco, line_axes,traço_cosseno, dot_cosseno, linha_v_traço, linha_h_traço, linha_auxiliar0,rótulo_v, rótulo_h, partícula_h, partícula_a) ELEMENTOS DO VÍDEO

        #self.add(n0, n1, n2, n3, n4)
        #self.add(retângulo)
        self.clear()
        self.wait()


----------------------------------------------------------------------------------------

# Cena 5

    %%manim -qh -v WARNING mostrar_coseno
    class mostrar_coseno(Scene):
        def construct(self):


        #*********************************************************************************************************************************************************
        axes = Axes(
        x_range = [-2,2,0.5],
        y_range = [-2,2,0.5],
        x_length = 4,
        y_length = 4,
        stroke_width  = 10

         ).set_width(8).set_opacity(0.3) # CRIA EIXOS PARA O CÍRCULO

        circle = Circle(radius = 1, stroke_color = GREEN, stroke_width = 8, ).set_width(4).set_stroke(opacity = 0.5) # cria írculo
        t =ValueTracker(2*PI)  # cria variável

        particula = Dot(axes.c2p(np.cos( t.get_value() ), np.sin( t.get_value() ) ), color = RED).set_width(0.25)  # CRIA PARTICULA

        arco = always_redraw( lambda: axes.plot_parametric_curve( lambda t: np.array(
                                                         [np.cos(t),np.sin(t)]
                                                         ),t_range = [0, t.get_value() ], color = RED ) )  # CRIA ARCO

        linha_auxiliar0 = Line( start = axes.c2p(-1,0), end = axes.c2p(1,0), color =  YELLOW, stroke_width = 8).set_opacity(0)
        linha_auxiliar0.rotate(angle = PI/2)
        grupo = VGroup( axes, circle , arco,linha_auxiliar0)  # grupo dos elementos base

        #*******************************************************  texto função cosseno
        func_b = always_redraw(lambda:  MathTex('b(s)').to_edge(LEFT + UP, buff = 1.5 ))
        igual = MathTex('=').next_to(func_b, RIGHT, buff = 0.5)
        func_seno = MathTex('sen(s)').next_to(igual, RIGHT, buff = 0.5)
        #*******************************************************

        #**********************************************************************************************************************************************************
        #**********************************************************************************************************************
        axes1 = Axes(x_range = [-8,8,PI/2], y_range = [-2,2,1], x_length = 10,y_length = 5).to_edge(LEFT + DOWN,buff = 0.2)# eixos do cos e sen
        axes2 =Axes( y_range = [-8,8,1], y_length = 8) # eixos auxiliares
        line_arco = Line( start = axes2.c2p(0,0), end = axes2.c2p(0,2*PI), color =  RED, stroke_width = 8) # Segmento Vertical
        line_axes = Line(start = axes1.c2p(2*PI,0),  end = axes1.c2p(0,0), color =  RED, stroke_width = 8) # Segmento horizontal
        line_axes_negativo = Line(start = axes1.c2p(0,0),  end = axes1.c2p(-2*PI,0), color =  RED, stroke_width = 8) # Segmento horizontal

        #********************* escala radianos positivos e negativos
        tnum = 0.8
        n0 = MathTex('0').next_to( axes1.c2p(0,0),UP + LEFT, buff = 0.2 ).scale(tnum)
        n1 = MathTex('\\frac{\\pi}{2}').next_to(axes1.c2p(PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        n2 = MathTex('\\pi').next_to(axes1.c2p(PI,0), UP, buff = 0.2 ).scale(tnum)
        n3 = MathTex('3\\frac{\\pi}{2}').next_to(axes1.c2p(3*PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        n4 = MathTex('2\\pi').next_to(axes1.c2p(2*PI,0), UP , buff = 0.2 ).scale(tnum)
        grupo_radianos = VGroup(n0, n1, n2, n3, n4)

        N1 = MathTex('-\\frac{\\pi}{2}').next_to(axes1.c2p(-PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        N2 = MathTex('-\\pi').next_to(axes1.c2p(-PI,0), UP, buff = 0.2 ).scale(tnum)
        N3 = MathTex('-3\\frac{\\pi}{2}').next_to(axes1.c2p(-3*PI/2,0), DOWN , buff = 0.2 ).scale(tnum)
        N4 = MathTex('-2\\pi').next_to(axes1.c2p(-2*PI,0), UP , buff = 0.2 ).scale(tnum)
        grupo_radianos_n = VGroup( N1, N2, N3, N4)
        #*********************

        #********************* Escala de Unidade
        Unidade0 = MathTex('1').next_to(axes1.c2p(0, 1), LEFT, buff = 0.2)
        Unidade1 = MathTex('-1').next_to(axes1.c2p(0, -1), LEFT, buff = 0.2)
        grupo_numérico = VGroup(Unidade0, Unidade1)
        #*********************


        #************************ ELEMENTOS DO TRAÇO DO SENO

        theta_p = ValueTracker(0)
        theta_n = ValueTracker(0)
        traço_seno = always_redraw(lambda: axes1.plot(lambda x: np.sin(x), x_range = [theta_n.get_value(),theta_p.get_value()], color = YELLOW) )
        dot_seno = always_redraw(lambda: Dot(axes1.c2p(theta_p.get_value(), np.sin(theta_p.get_value()))) )
        dot_seno_n = always_redraw(lambda: Dot(axes1.c2p(theta_n.get_value(), np.sin(theta_n.get_value()))) )
        linha_h_traço = always_redraw( lambda: axes1.get_horizontal_line( dot_seno.get_center() , line_func = Line) )
        linha_v_traço = always_redraw( lambda: axes1.get_vertical_line( dot_seno.get_center() , line_func = Line) )
        linha_auxiliar1 = Line( start = axes1.c2p(0,-1), end = axes1.c2p(0, 1), color = YELLOW, stroke_width = 8 )

        #******************************************************************************************************* RÓTULOS DA FUNÇÃO COSSENO
        rótulo_v = MathTex('b').next_to(axes1, UP, buff = -0.4).shift(0.6*LEFT).set_color(YELLOW).scale(1.5)
        rótulo_h =  MathTex('s').next_to(axes1, RIGHT, buff = -0.4).shift(0.6*DOWN).set_color(RED).scale(1.5)
        #*******************************************************************************************************

        partícula_h = always_redraw(lambda: Dot(axes1.c2p(theta_p.get_value(),0)).set_color(RED).scale(1.3) )
        partícula_a = always_redraw(lambda: Dot(axes1.c2p(0, np.sin(theta_p.get_value()))).set_color(YELLOW).scale(1.3) )

        partícula_hn = always_redraw(lambda: Dot(axes1.c2p(theta_n.get_value(),0)).set_color(RED).scale(1.3) )
        partícula_an = always_redraw(lambda: Dot(axes1.c2p(0, np.sin(theta_n.get_value()))).set_color(YELLOW).scale(1.3) )


        #********************************************************************************************************
        retângulo = RoundedRectangle(corner_radius = 0.1,stroke_color = WHITE, stroke_width = 3,
                               height = 0.5, width  = 2).shift(UP+RIGHT*4)
        retângulo.rotate(angle = PI/2)

        grupo.shift(4*RIGHT + UP).set_width(3)
        #****************************************************************************************************************

        ####################################################################################################################################### COMEÇO DO VÍDEO

        self.add(grupo)
        self.play(LaggedStart( Write(func_b),Write(igual),Write(func_seno)), lag_ratio = 0.5, run_time = 2)

        ######################################################### preparando elementos para plotar o gráfico positivo
        self.wait()
        self.play( Write (axes1) )
        self.play( Write (rótulo_h), Write (rótulo_v) )
        self.play( ReplacementTransform (arco,line_arco))
        self.play( ReplacementTransform (line_arco,line_axes) )
        self.play( FadeOut (line_axes), Write(grupo_radianos) )
        self.play( Create (retângulo) )
        self.play( linha_auxiliar0.animate.set_opacity(1) )
        self.play( FadeOut (retângulo), ReplacementTransform( linha_auxiliar0, linha_auxiliar1) )
        self.play( FadeOut (linha_auxiliar1))
        self.play( Write (grupo_numérico) )
        self.add ( dot_seno)
        self.play( FadeIn(traço_seno), FadeIn(partícula_h), FadeIn(partícula_a) )

        #********************************************************************************
        lineHp = always_redraw( lambda: axes1.get_horizontal_line( dot_seno.get_center() , line_func = Line) )
        lineVp = always_redraw( lambda: axes1.get_vertical_line( dot_seno.get_center() , line_func = Line) )
        #********************************************************************************
        self.add(lineHp, lineVp)

        ############################################################################################################

        ############################################################## Cria gráfico cosseno parte positiva
        self.play( theta_p.animate.set_value(PI/2), run_time = 2 )
        self.play( theta_p.animate.set_value(PI), run_time = 2)
        self.play( theta_p.animate.set_value( 3*(PI/2)), run_time = 2)
        self.play( theta_p.animate.set_value(2*PI) , run_time = 2)
        self.play( FadeOut( lineHp, lineVp, dot_seno))
        #######################################################################################################

        #*******************************************************
        traço_cópia = traço_seno.copy()
        #*******************************************************

        self.play( FadeOut(traço_seno),FadeOut(partícula_a),FadeOut(partícula_h))

        #*******************************************************
        theta_p.set_value(0)
        #*******************************************************

        ######################################################## preparando elementos para plotar o gráfico negativo
        self.play(FadeIn(arco))
        self.play( ReplacementTransform (arco,line_arco))
        self.play( ReplacementTransform (line_arco,line_axes_negativo) )
        self.play( FadeOut( line_axes_negativo) )
        self.play(  Write (grupo_radianos_n))
        self.add(dot_seno_n)

        #********************************************************************************
        lineHn = always_redraw( lambda: axes1.get_horizontal_line( dot_seno_n.get_center() , line_func = Line) )
        lineVn = always_redraw( lambda: axes1.get_vertical_line( dot_seno_n.get_center() , line_func = Line) )
        #********************************************************************************
        self.add(lineHn, lineVn)

        ########################################################

        ############################################################## Cria gráfico cosseno parte negativa
        self.add ( traço_seno )
        self.add ( partícula_an, partícula_hn)
        self.play( theta_n.animate.set_value(-2*PI), run_time = 4)
        self.play( FadeOut( lineHn, lineVn, dot_seno_n))
        #############################################################

        ############################################################# Finaliza gráfico Cosseno

        self.play(FadeIn (traço_cópia), FadeOut(partícula_an, partícula_hn), run_time = 3)


        ############################################################################################################################################################################
        #self.add( axes1, line_arco, line_axes,traço_cosseno, dot_cosseno, linha_v_traço, linha_h_traço, linha_auxiliar0,rótulo_v, rótulo_h, partícula_h, partícula_a) ELEMENTOS DO VÍDEO

        #self.add(n0, n1, n2, n3, n4)
        #self.add(retângulo)

        self.wait()





