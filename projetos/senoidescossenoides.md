## Cena 1

```python

    %%manim -qm -v WARNING senoide_estatica1

    class senoide_estatica1(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A sin(\omega  t +\\phi)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A cos(\omega  t +\\phi)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(x)

    def f2(x):
      return Ac2.get_value()*np.cos(x)

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.3*DOWN) )
    c1 = E1.plot(lambda x: f1(x), x_range = [-7,7], color = YELLOW)


    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.3*DOWN) )
    c2 = E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW)

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Text('A - Amplitude').move_to([0,3,0])
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    def cobrir_cena(x):
      retangulo = Rectangle().scale(2).set_opacity(0.7).set_color(BLACK)
      if x ==1:
        return self.play(FadeIn(retangulo))
      if x ==0:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])

    # n17 criar contador numérico
    n17 = DecimalNumber(1)
    n17.add_updater(lambda d: d.set_value(w2.get_value()))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.6)
    n18 = VGroup(n18_0, n18_1)

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Text(' - Velocidade Angular').next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Text(' - Frequência Angular ').next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Text('N° de ciclos que')
    n35_1 = Text('ocorrem em 1 segundo ').next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Text(' - Ângulo de Fase ').next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.6)
    n40 = VGroup(n40_0, n40_1)

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.6)
    n42 = VGroup(n42_0, n42_1)

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')

    L1 = E2.get_vertical_line(E2.i2gp(2*PI, c2 ), color=YELLOW)


    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################


    text0 = Tex('\\textsc{POWER VISUALS}').shift(UP).set_width(8).set_color_by_gradient(YELLOW, BLUE)
    text00 = Tex('\\textit{ Apresenta}').shift(DOWN).set_width(3)
    self.wait()
    self.play(Write(text0))
    self.wait(0.5)

    self.play(Write(text00))
    self.play(Unwrite(text0), run_time = 0.5)
    self.play(Unwrite(text00),run_time = 0.5)


    g1 = VGroup(n1, n2)
    self.play(Write(g1))
    g2 = VGroup(n3, n4)
    self.play(Write(g2))


    self.wait(7)
    self.play(Write(n5))  #ok
    self.wait(4)
    self.wait(7)
    g3 = VGroup(n1,n2,n3,n4,n5)
    self.play(FadeOut(g3))

    g4 = VGroup(ne4,n6)
    self.play(Write(g4), run_time = 2)
    self.wait(2)
    self.play(Write(n7))
    self.wait(2)
    self.play(Unwrite(n7))
    self.play(FadeOut(ne4), run_time = 2)
    self.wait(1.5)
    self.play(n6.animate.move_to([0,0,0]), run_time = 2)
    self.wait(13)

    self.play(Write(n8))
    self.wait()
    self.play(ReplacementTransform(n6, n9), run_time = 2)
    self.wait()
    g5 = VGroup(n8,n9)
    self.play(FadeOut(g5))

```
------------------------------------------------------------------------------------

# Cena 2

```python
    %%manim -qm -v WARNING senoide_estatica2
    
    class senoide_estatica2(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(x)

    def f2(x):
      return Ac2.get_value()*np.cos(x)

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN) )
    c1 = E1.plot(lambda x: f1(x), x_range = [-7,7], color = BLUE)


    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW)

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Text('A - Amplitude').move_to([0,3,0])
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    def cobrir_cena(x):
      retangulo = Rectangle().scale(2).set_opacity(0.7).set_color(BLACK)
      if x ==1:
        return self.play(FadeIn(retangulo))
      if x ==0:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0])

    # n17 criar contador numérico
    n17 = DecimalNumber(1)
    n17.add_updater(lambda d: d.set_value(w2.get_value()))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.6)
    n18 = VGroup(n18_0, n18_1)

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Text(' - Velocidade Angular').next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Text(' - Frequência Angular ').next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Text('N° de ciclos que')
    n35_1 = Text('ocorrem em 1 segundo ').next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Text(' - Ângulo de Fase ').next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.6)
    n40 = VGroup(n40_0, n40_1)

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.6)
    n42 = VGroup(n42_0, n42_1)

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')

    L1 = E2.get_vertical_line(E2.i2gp(2*PI, c2 ), color=YELLOW)


    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################

    # cena 4

    #self.add(n10)
    #self.add(n11)
    #self.add(E1)
    #self.add(c1)

    n7.move_to([-3.5,-3,0])
    #self.add(n7)
    n6.move_to([-1.5,2,0])
    #self.add(n6)


    #self.add(n12)
    #self.add(n13)
    #self.add(E2)
    #self.add(c2)
    n5.move_to([3.5,-3,0])
    #self.add(n5)
    n9.move_to([5.3,2,0])
    #self.add(n9)
    G1.shift(0.5*LEFT)

    g6 = VGroup(E1,n10,n11)
    self.play(DrawBorderThenFill(g6))
    self.play(Write(n6), run_time = 1.5)
    self.play(Write(c1), run_time = 1.5)
    self.play(Write(n7))

    g7 = VGroup(E2,n12,n13)
    self.play(DrawBorderThenFill(g7))
    self.play(Write(n9))
    self.play(Write(c2))
    self.play(Write(n5))
```
------------------------------------------------------------------------------------

# Cena 3
```python
    %%manim -qm -v WARNING senoide_estatica3
    
    class senoide_estatica3(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(x)

    def f2(x):
      return Ac2.get_value()*np.cos(x)

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN) )
    c1 = always_redraw(lambda: E1.plot(lambda x: f1(x), x_range = [-7,7], color = BLUE))


    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = always_redraw(lambda:E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW))

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Tex('\\textit{A - Amplitude}').move_to([0,3,0]).scale(1.5)
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02).set_color_by_gradient([YELLOW, WHITE])
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.
    ######################################################### Plano que cobre a cena
    retangulo = Rectangle().scale(4).set_opacity(0.9).set_color(BLACK).move_to([0,0,1])
    def cobrir_cena(x):
      if x ==1:
        return self.play(FadeIn(retangulo))
      else:
        return self.play(FadeOut(retangulo))
    #################################################################################


    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])

    # n17 criar contador numérico
    n17 = DecimalNumber(1)
    n17.add_updater(lambda d: d.set_value(w2.get_value()).scale(0.5))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.6)
    n18 = VGroup(n18_0, n18_1)

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Text(' - Velocidade Angular').next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Text(' - Frequência Angular ').next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Text('N° de ciclos que')
    n35_1 = Text('ocorrem em 1 segundo ').next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Text(' - Ângulo de Fase ').next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.6)
    n40 = VGroup(n40_0, n40_1)

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.6)
    n42 = VGroup(n42_0, n42_1)

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')

    L1 = E2.get_vertical_line(E2.i2gp(2*PI, c2 ), color=YELLOW)


    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################

    ##################### imagem da cena 4(atualize este código)
    self.add(n10)
    self.add(n11)
    self.add(E1)
    self.add(c1)
    n7.move_to([-3.5,-3,0])
    self.add(n7)
    n6.move_to([-1.5,1.5,0])
    self.add(n6)


    self.add(n12)
    self.add(n13)
    self.add(E2)
    self.add(c2)
    n5.move_to([3.5,-3,0])
    self.add(n5)
    n9.move_to([5.3,1.5,0])
    self.add(n9)
    #############################################################

    #self.add(ne) # rótulo da amplitude
    G0.shift(0.5*LEFT)
    G1.shift(1.5*LEFT)

    # n14 criar contador numérico


    n141 = MathTex('1').next_to(ne01, RIGHT, buff = 0.1)
    n142 = MathTex('2').next_to(ne01, RIGHT, buff = 0.1)
    n1406 = MathTex('0.6').next_to(ne01, RIGHT, buff = 0.1)
    n140 = MathTex('0').next_to(ne01, RIGHT, buff = 0.1)
    n14m1 = MathTex('-1').next_to(ne01, RIGHT, buff = 0.1)
    n141m = MathTex('1').next_to(ne01, RIGHT, buff = 0.1)


    #self.add(ne1) # rótulo da cossenoide com amplitude variável

    #self.add(n14)


    self.play(Write(ne), run_time = 2)
    self.play(ReplacementTransform(n9, ne1), run_time = 1.5)
    self.play(Write(n141), run_time = 1.5)
    self.wait(9)

    self.play(Ac2.animate.set_value(2), Transform(n141,n142), run_time = 5)

    self.play(Ac2.animate.set_value(0.6),Transform(n141,n1406), run_time = 4)

    self.play(Ac2.animate.set_value(0), Transform(n141,n140))

    self.play(Ac2.animate.set_value(-1),Transform(n141,n14m1), run_time = 4)

    self.play(Ac2.animate.set_value(1),Transform(n141,n141m), run_time = 4 )

    self.wait()
    cobrir_cena(1)
    self.wait(8)
    self.play(Write(n15))
    self.wait(3)
    self.play(ReplacementTransform(n15, n16), run_time = 3)
    self.wait(6)
    self.play(FadeOut(n16), run_time = 2)
    self.remove(ne,n141,ne1)



    cobrir_cena(0)
    self.wait()

```
------------------------------------------------------------------------------------

# Cena 4
```python
    %%manim -qm -v WARNING senoide_estatica04
    
    class senoide_estatica04(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(x)

    def f2(x):
      return Ac2.get_value()*np.cos(w2.get_value()*x)

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN) )
    c1 = E1.plot(lambda x: f1(x), x_range = [-7,7], color = BLUE)


    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = always_redraw(lambda: E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW))

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Tex('\\textit{A - Amplitude}').move_to([0,3,0]).scale(1.5)
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    retangulo = Rectangle().scale(4).set_opacity(0.9).set_color(BLACK).move_to([0,0,1])
    def cobrir_cena(x):
      if x ==1:
        return self.play(FadeIn(retangulo))
      else:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1).scale(0.7)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0])

    # n17 criar contador numérico
    n17 = DecimalNumber(0)
    n17.add_updater(lambda d: d.set_value(w2.get_value()).scale(0.5))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.75)
    n18 = VGroup(n18_0, n18_1).set_color_by_gradient([YELLOW, WHITE])

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Tex('\\textit {- Velocidade Angular}').scale(1.5).next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n24 = MathTex('\\omega').move_to([-0.5,0,0]).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n25 =  MathTex('=').scale(2).set_color_by_gradient([WHITE,GREEN_E]).next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').scale(2).set_color_by_gradient([WHITE,GREEN_E]).next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.3*RIGHT).scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n30 = MathTex('T').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Text(' - Frequência Angular ').next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Text('N° de ciclos que')
    n35_1 = Text('ocorrem em 1 segundo ').next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Text(' - Ângulo de Fase ').next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.6)
    n40 = VGroup(n40_0, n40_1)

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.6)
    n42 = VGroup(n42_0, n42_1)

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')

    L1 = E2.get_vertical_line(E2.i2gp(2*PI, c2 ), color=YELLOW)

    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################
    #cena 9

    ############################## cena 4(atualize este código)

    self.add(n10)
    self.add(n11)
    self.add(E1)
    self.add(c1)
    n7.move_to([-3.5,-3,0])
    self.add(n7)
    n6.move_to([-1.5,2,0])
    self.add(n6)


    self.add(n12)
    self.add(n13)
    self.add(E2)
    self.add(c2)
    n5.move_to([3.5,-3,0])
    self.add(n5)
    n9.move_to([5.3,2,0])
    #self.add(n9)
    ###########################################################
    G0.shift(0.5*LEFT)
    G1.shift(1.5*LEFT)
    #self.add(n18)
    #self.add(n19)


    self.play(FadeIn(n9))
    self.wait(2)
    self.play(Write(n19), run_time = 4)
    n9_1= n9.copy()
    self.play(Transform(n9, n18))

    # n17 criar contador numérico


    n171 = MathTex('1').next_to(n18_0, RIGHT, buff = 0.1)
    n172 = MathTex('2').next_to(n18_0, RIGHT, buff = 0.1)
    n1702 = MathTex('0.2').next_to(n18_0, RIGHT, buff = 0.1)
    n171m = MathTex('1').next_to(n18_0, RIGHT, buff = 0.1)


    self.play(Write(n171))

    self.wait(6)

    self.play(w2.animate.set_value(2), Transform(n171,n172), run_time = 6)
    self.wait(5)

    self.play(w2.animate.set_value(0.2),Transform(n171,n1702), run_time =5)
    self.wait(4)

    self.play(w2.animate.set_value(1), Transform(n171,n171m))

    self.play(Unwrite(n19))




    ## criar curvas verdes
    c1verde = E1.plot( lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10)
    c2verde = always_redraw(lambda: E2.plot(lambda x: f2(x), x_range = [0,2*PI/w2.get_value()], color = GREEN,stroke_width = 10))

    self.play( FadeIn(c1verde), FadeIn(c2verde) )

    # criar linhas verticais

    n172 = MathTex('2').next_to(n18_0, RIGHT, buff = 0.1)
    self.play(w2.animate.set_value(2), Transform(n171,n172), run_time = 4)

    lineV1 = always_redraw( lambda: E1.get_vertical_line( E1.c2p(2*PI,f1(2*PI))  , line_func = Line) )
    lineV2 = always_redraw( lambda: E2.get_vertical_line( E2.c2p(PI,f2(2*PI)) , line_func = Line) )

    doispi = MathTex('2 \\pi').next_to( E1.c2p(2*PI,0) , DOWN, buff = 0.1)
    pi     = MathTex('\\pi').next_to( E2.c2p(PI,0) , DOWN, buff = 0.1)

    self.play(Create(lineV1), Create(lineV2))
    self.play(Write(doispi), Create(pi))

    cobrir_cena(1)
    self.remove(c1verde, c2verde, doispi, pi,lineV1, lineV2)
    self.wait()
    self.play(Write(n22), run_time= 3)
    self.wait()
    self.play(Transform(n22, n23), run_time= 3)
    self.wait(2)
    self.play(Transform(n22, n24), run_time = 3)
    g2 = VGroup(n25,n26)
    self.play(Write(g2))
    self.play(Transform(n26, n28), run_time = 2)
    self.wait(10)
    g3 = VGroup(n22,n25,n26)
    self.play(FadeOut(g3), run_time = 4)
    cobrir_cena(0)
    self.wait(4)

    self.play(FadeOut(G0), FadeOut(n7),FadeOut(n5))

    G11 = VGroup(G1, n171,n18_0)
    self.play(G11.animate.move_to([0,0,0]), run_time = 3)
    n172 = MathTex('1').next_to(n18_0, RIGHT, buff = 0.1)

    self.play( w2.animate.set_value(1), Transform(n171,n172) )

```
------------------------------------------------------------------------------------

# Cena 5
```python
    %%manim -qm -v WARNING senoide_estatica05
    
    class senoide_estatica05(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(x)

    def f2(x):
      return Ac2.get_value()*np.cos(w2.get_value()*x)

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN) )
    c1 = E1.plot(lambda x: f1(x), x_range = [-7,7], color = BLUE)


    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = always_redraw(lambda: E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW))

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Tex('\\textit{A - Amplitude}').move_to([0,3,0]).scale(1.5)
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    retangulo = Rectangle().scale(4).set_opacity(0.9).set_color(BLACK).move_to([0,0,1])
    def cobrir_cena(x):
      if x ==1:
        return self.play(FadeIn(retangulo))
      else:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1).scale(0.7)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0])

    # n17 criar contador numérico
    n17 = DecimalNumber(0)
    n17.add_updater(lambda d: d.set_value(w2.get_value()).scale(0.5))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.75)
    n18 = VGroup(n18_0, n18_1).set_color_by_gradient([YELLOW, WHITE])

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Tex('\\textit {- Velocidade Angular}').scale(1.5).next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{T}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28).set_color_by_gradient([WHITE,GREEN_E])
    G2 = VGroup(n24,n25,n32).set_color_by_gradient([WHITE,GREEN_E])


    n34_0 = MathTex('f').scale(2)
    n34_1 = Tex(' - Frequência Angular ').scale(1.5).next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Tex('N° de ciclos que').scale(1.5)
    n35_1 = Tex('ocorrem em 1 segundo ').scale(1.5).next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}').scale(2).set_color_by_gradient([WHITE,GREEN_E])
    n39 = MathTex('\\omega = 2 \\pi f').scale(2).set_color_by_gradient([WHITE,GREEN_E])

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Text(' - Ângulo de Fase ').next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.6)
    n40 = VGroup(n40_0, n40_1)

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.6)
    n42 = VGroup(n42_0, n42_1)

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')

    L1 = E2.get_vertical_line(E2.i2gp(2*PI, c2 ), color=YELLOW)

    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################

    #cena 8 e cena 9
    ############################## cena 4(atualize este código)
    self.add(n12)
    self.add(n13)
    self.add(E2)
    self.add(c2)
    n5.move_to([3.5,-3,0])

    n9.move_to([5.3,2,0])
    #self.add(n9)
    ###########################################################
    G1.shift(1.5*LEFT)
    self.add(n18)

    G1_anterior = G1.copy()
    G11 = VGroup(G1,n18)
    G11.move_to([0,0,0])
    n172 = MathTex('1').next_to(n18_0, RIGHT, buff = 0.1)
    self.add(n172)

    ##############################################################################


    n30.next_to(E2.c2p(0,0,0), RIGHT+1.7*DOWN, buff = 0.5)
    #self.add(n30) # construir rótulo da seta: período

    G02.move_to([3,-1.5,0])
    #self.add(G02)

    n31.next_to(n25, RIGHT, buff = 0.2)
    #self.add(n31)
    n32.next_to(n25, RIGHT, buff = 0.2)
    n33.move_to(G02.get_center())
    #self.add(n33)
    n34.move_to([0,2.6,0])
    n37.move_to([0,-2.3,0])


    L1 = Line(start = E2.c2p(2*PI, f2(2*PI)) , end = E2.c2p(2*PI, -1.2*f2(2*PI)) )
    v1_0 = Arrow(E2.c2p(PI,1.2*f2(PI)),E2.c2p(0,-1.2), buff=0)
    v1_1 = Arrow(E2.c2p(PI,1.2*f2(PI)),E2.c2p(2*PI,-1.2), buff=0)
    v1 = VGroup(v1_0, v1_1)

    self.play(FadeIn(v1))
    self.play(Write(L1))
    self.play(Write(n30))
    self.wait(7)
    self.play(Write(n24))
    self.play(Write(n25))
    self.play(Write(n28))
    self.wait(2)
    self.play(Transform(n28, n31))
    self.play(Transform(n28, n32))
    self.play(Transform(G02, n33))  # parei aqui

    cobrir_cena(1)

    self.play( Write(n34))
    self.play( Write(n35))
    g2 = VGroup( n34,n35)
    self.play( Unwrite(g2))
    self.play( Write(n36))
    self.play( Write(n37))

    self.play( n37.animate.move_to(n36))
    self.play(FadeOut(n37))
    self.play( Transform(n36, n38))

    self.play( Transform(n36, n39))
    self.play( FadeOut(n36))

    # antes descobrir a cena remover alguns objetos e prepara a tela para a cena 16
    # da defasagem angular!
    ### faça isso aqui!!
    self.remove(n30,v1,L1,G02,n18,n172)
    cobrir_cena(0)

    n5.move_to([3.5,-3,0])
    n6.move_to([-1.5,2,0])
    n7.move_to([-3.5,-3,0])
    self.play( FadeIn(G0), G1.animate.move_to(G1_anterior.get_center()), FadeIn(n5), FadeIn(n7) )

```

------------------------------------------------------------------------------------

# Cena 6
```python

    %%manim -qm -v WARNING senoide_estatica06
    
    class senoide_estatica06(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(w1.get_value()*x + phic1.get_value())

    def f2(x):
      return Ac2.get_value()*np.cos(w2.get_value()*x + phic2.get_value())

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = always_redraw(lambda: MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n11 = always_redraw(lambda: MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN) )
    c1 = always_redraw(lambda: E1.plot(lambda x: f1(x), x_range = [-7,7], color = BLUE))




    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = always_redraw(lambda: E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW))

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Tex('\\textit{A - Amplitude}').move_to([0,3,0]).scale(1.5)
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    retangulo = Rectangle().scale(4).set_opacity(0.9).set_color(BLACK).move_to([0,0,1])
    def cobrir_cena(x):
      if x ==1:
        return self.play(FadeIn(retangulo))
      else:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1).scale(0.7)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0])

    # n17 criar contador numérico
    n17 = DecimalNumber(1)
    n17.add_updater(lambda d: d.set_value(w2.get_value()).scale(0.5))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.6)
    n18 = VGroup(n18_0, n18_1)

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Text(' - Velocidade Angular').next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Tex(' - Frequência Angular ').scale(1.5).next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Tex('N° de ciclos que').scale(1.5)
    n35_1 = Tex('ocorrem em 1 segundo ').scale(1.5).next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Tex(' - Ângulo de Fase ').scale(1.5).next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.8)
    n40 = VGroup(n40_0, n40_1).set_color_by_gradient([BLUE, WHITE])

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t ')
    n42_1 = MathTex(' )').next_to(n42_0, RIGHT, buff = 0.8)
    n42 = VGroup(n42_0, n42_1).set_color_by_gradient([YELLOW, WHITE])

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ')
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ')
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ')



    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################

     # cena 16


    ########################################################### cena 9(atualize este código)
    ############################## cena 4(atualize este código)
    self.add(n10)
    self.add(n11)
    self.add(E1)
    self.add(c1)
    n7.move_to([-3.5,-3,0])
    self.add(n7)
    n6.move_to([-1.5,2,0])
    self.add(n6)


    self.add(n12)
    self.add(n13)
    self.add(E2)
    self.add(c2)
    n5.move_to([3.5,-3,0])
    self.add(n5)
    n9.move_to([5.3,2,0])
    self.add(n9)
    ###########################################################
    G0.shift(0.5*LEFT)
    G1.shift(1.5*LEFT)
    #self.add(n18)

    ###################################################################################

    ne3.move_to([0,3,0])
    #self.add(ne3)
    n40.move_to(n6.get_center()+0.5*DOWN).scale(0.8)
    n42.move_to(n9.get_center()+0.5*DOWN+0.2*RIGHT).scale(0.8)
    #self.add(n40)
    #self.add(n42)
    n44.move_to(E1.c2p(-2,-1.9,0))
    n45.move_to(E1.c2p(2,-1.9,0))

    n46.move_to(E2.c2p(-2,-1.9,0))
    n47.move_to(E2.c2p(2,-1.9,0))
    #self.add(n44, n45, n46, n47)
    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    #self.add(v2,v3,v4,v5)

    # n411 a n434 criar contador numérico

    n411 = MathTex('+0').scale(0.8).next_to(n40_0, RIGHT, buff = 0.1)
    n412 = MathTex('+2').scale(0.8).next_to(n40_0, RIGHT, buff = 0.1)
    n413 = MathTex('+0').scale(0.8).next_to(n40_0, RIGHT, buff = 0.1)
    n414 = MathTex('-2').scale(0.8).next_to(n40_0, RIGHT, buff = 0.1)

    n431 = MathTex('+0').scale(0.8).next_to(n42_0, RIGHT, buff = 0.1)
    n432 = MathTex('+2').scale(0.8).next_to(n42_0, RIGHT, buff = 0.1)
    n433 = MathTex('+0').scale(0.8).next_to(n42_0, RIGHT, buff = 0.1)
    n434 = MathTex('-2').scale(0.8).next_to(n42_0, RIGHT, buff = 0.1)

    self.wait(3)
    self.play(Write(ne3), run_time = 3)
    self.wait(2)

    self.play(Transform(n6, n40),FadeIn(n411), run_time =2)
    self.wait(2)
    self.play(Transform(n9, n42),FadeIn(n431), run_time =2)
    self.wait(10)

    self.play( Transform(n411,n412), Transform(n431,n432), run_time = 4)
    self.play( phic1.animate.set_value(2.5),FadeIn(v2),FadeIn(n44),phic2.animate.set_value(2.5),FadeIn(v4),FadeIn(n46), run_time= 4)
    self.wait(10)
    self.play( Transform(n411,n413), Transform(n431,n433), run_time = 2 )
    self.play( phic1.animate.set_value(0),FadeOut(v2),FadeOut(n44),phic2.animate.set_value(0),FadeOut(v4),FadeOut(n46) )
    self.wait()
    self.play( Transform(n411,n414), Transform(n431,n434), run_time = 2 )
    self.play( phic1.animate.set_value(-2.5),FadeIn(v3),FadeIn(n45),phic2.animate.set_value(-2.5),FadeIn(v5),FadeIn(n47), run_time = 2)
    self.wait(7)

    g1 = VGroup(v3,v5,n45,n47,G0,G1,n5,n7,ne3,n411,n431)
    self.play(FadeOut(g1))
```
------------------------------------------------------------------------------------

# Cena 7
```python

    %%manim -qm -v WARNING senoide_estatica07
    
    class senoide_estatica07(Scene):
      def construct(self):

    ##############################################################################
    #                    CRIAR OBJETOS MANIM
    ##############################################################################
    Ac1 = ValueTracker(1) # rastreador da amplitude c1
    w1  = ValueTracker(1)
    phic1 = ValueTracker(0)

    Ac2 = ValueTracker(1) # rastreador da amplitude c2
    w2  = ValueTracker(1)
    phic2 = ValueTracker(0)


    n1 = MathTex('f(t) = A \cdot  sin(\omega \cdot t)').move_to([-3,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n2 = MathTex('g(t) = A \cdot  cos(\omega \cdot t)').move_to([3.5,1.5,0]).set_color_by_gradient([RED, WHITE]).scale(1.2)
    n3 = Tex('\\textit{Senoides}', color = YELLOW).move_to([-3,-0.5,0]).scale(1.5)

    n4 = Tex('\\textit{Cossenoides}', color = YELLOW).move_to([3.5,-0.5,0]).scale(1.5)
    n5 = Tex('\\textsc{Domínio do tempo}', opacity = 1).move_to([0,-2.5,0]).set_color_by_gradient([GRAY, WHITE])

    ne4 = MathTex('F( \\theta)=sin( \\theta)').move_to([-3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n6 =  MathTex('G( \\theta)=cos( \\theta)').move_to([3,1.5,0]).scale(1.2).set_color_by_gradient([BLUE, WHITE])
    n7 =  Tex('\\textsc{Domínio do Ângulo}').move_to([0,-1,0]).set_color_by_gradient([GRAY, WHITE])
    n8 =  Tex('\\textit{Mudar Domínio}').move_to([0,-2,0]).scale(1.5)
    n9 =  MathTex('G(t)=cos(t)').move_to([0,0,0]).set_color_by_gradient([YELLOW, WHITE]).scale(1.2)



    def f1(x):
      return Ac1.get_value()*np.cos(w1.get_value()*x + phic1.get_value())

    def f2(x):
      return Ac2.get_value()*np.cos(w2.get_value()*x + phic2.get_value())

    E1  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([-3.5,0,0])
    n10 = MathTex('y').next_to( E1, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN)
    n11 = MathTex('\\theta').next_to( E1, RIGHT, buff = 0).shift(0.5*DOWN)
    c1 =  always_redraw(lambda: E1.plot(lambda x: f1(x), x_range = [-7,7], color = YELLOW))

    E2  = Axes(x_range = [-9,9,2], y_range = [-2,3,1] , x_length = 4, y_length = 3).move_to([3.5,0,0])
    n12 = always_redraw(lambda: MathTex('y').next_to( E2, UP, buff = 0 ).shift(0.3*LEFT+0.2*DOWN) )
    n13 = always_redraw(lambda: MathTex('t').next_to( E2, RIGHT, buff = 0).shift(0.5*DOWN) )
    c2 = always_redraw(lambda: E2.plot(lambda x: f2(x), x_range = [-7,7], color = YELLOW))

    G0 = VGroup(E1,n10,n11,n6, c1)
    G1 = VGroup(E2, n12,n9,n13, c2)

    ne =  Tex('\\textit{A - Amplitude}').move_to([0,3,0]).scale(1.5)
    ######################################################### Equação envolvendo amplitude
    ne01 = MathTex('A \\cdot G(t)=').move_to([3.4,1.5,0])
    ne02 = MathTex('cos(t)').next_to(ne01, RIGHT, buff = 0.7)
    ne1 = VGroup(ne01,ne02)
    #########################################################
    # CRIAR OBJETO n14. OBJETO QUE SIMULA UMA CONTAGEM NUMÉRICA NA TELA.

    ######################################################### Plano que cobre a cena
    retangulo = Rectangle().scale(4).set_opacity(0.7).set_color(BLACK).move_to([0,0,1])
    def cobrir_cena(x):
      if x ==1:
        return self.play(FadeIn(retangulo))
      else:
        return self.play(FadeOut(retangulo))
    #################################################################################
    # n14 criar contador numérico
    n14 = DecimalNumber(1).scale(0.7)
    n14.add_updater(lambda d: d.set_value(Ac2.get_value()))

    n15 = MathTex('-1\leqslant  cos(t)\leqslant 1').move_to([0,0,0])
    n16 = MathTex('-A\leqslant  A\cdot cos(t)\leqslant A').move_to([0,0,0])

    # n17 criar contador numérico
    n17 = DecimalNumber(1)
    n17.add_updater(lambda d: d.set_value(w2.get_value()).scale(0.5))




    n18_0 = MathTex('G(\\omega \\cdot t)=cos(').move_to([3.8,1.8,0])
    n18_1 = MathTex('t)').next_to(n18_0, RIGHT, buff = 0.6)
    n18 = VGroup(n18_0, n18_1)

    n19_0 =  MathTex('\\omega').move_to([-3,3,0]).scale(2)
    n19_1 =  Text(' - Velocidade Angular').next_to(n19_0, RIGHT, buff = 0.2)
    n19 = VGroup(n19_0,n19_1)

    caux1=E1.plot(lambda x: f1(x), x_range = [0,2*PI], color = GREEN, stroke_width = 10 )
    caux2=E2.plot(lambda x: f2(x), x_range = [0,(2*PI)/w2.get_value()], color = GREEN, stroke_width = 10)

    n22 = MathTex('G(\\theta) = G(\\omega \\cdot t)').move_to([0,0,0])
    n23 = MathTex('\\theta =\\omega \\cdot t').move_to([0,0,0])
    n24 = MathTex('\\omega').move_to([-0.5,0,0])
    n25 =  MathTex('=').next_to(n24, RIGHT, buff = 0.2)
    n26 =  MathTex('\\frac{\\theta}{t}').next_to(n25, RIGHT, buff = 0.2)
    n28 =  MathTex('\\frac{\\bigtriangleup \\theta }{\\bigtriangleup t }').move_to(n26.get_center()+0.2*RIGHT)
    n30 = MathTex('T')
    n31 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n32 = MathTex('\\frac{2 \\pi}{\\bigtriangleup t}')
    n33 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    G02 = VGroup(n24,n25,n28)
    G2 = VGroup(n24,n25,n32)


    n34_0 = MathTex('f').scale(2)
    n34_1 = Tex(' - Frequência Angular ').scale(1.5).next_to(n34_0, RIGHT, buff = 0.2)
    n34 = VGroup(n34_0, n34_1)


    n35_0 = Tex('N° de ciclos que').scale(1.5)
    n35_1 = Tex('ocorrem em 1 segundo ').scale(1.5).next_to(n34_0, DOWN, buff = 0.2)
    n35 = VGroup(n35_0, n35_1)

    n36 = MathTex('f = \\frac{1}{T}')
    n37 = MathTex('T = \\frac{2 \\pi}{\\omega}')
    n38 = MathTex('f = \\frac{\\omega}{2 \\pi}')
    n39 = MathTex('\\omega = 2 \\pi f')

    ne3_0 = MathTex('\\phi').scale(2)
    ne3_1 = Tex(' - Ângulo de Fase ').scale(1.5).next_to(n34_0, RIGHT, buff = 0.2)
    ne3= VGroup(ne3_0, ne3_1)

    n40_0 = MathTex('G(\\theta + \\phi) = cos(\\theta ')
    n40_1 = MathTex(' )').next_to(n40_0, RIGHT, buff = 0.8)
    n40 = VGroup(n40_0, n40_1).set_color_by_gradient([BLUE, WHITE])

    # criar n41 contador
    n41 = DecimalNumber(0)
    n41.add_updater(lambda d: d.set_value(w1.get_value()))

    n42_0 = MathTex('G(t +\\phi) = cos(t')
    n42_1 = MathTex('+\\phi )').next_to(n42_0, RIGHT, buff = 0)
    n42 = VGroup(n42_0, n42_1).set_color_by_gradient([YELLOW, WHITE])

    # criar n43 contador
    n43 = DecimalNumber(0)
    n43.add_updater(lambda d: d.set_value(w1.get_value()))


    n44 = MathTex('\\phi')
    n45 = MathTex('\\phi')
    n46 = MathTex('\\phi')
    n47 = MathTex('\\phi')

    # criar v2 v3 v4 v5
    v1_0 = Arrow([0,0,0],[-1,0,0], buff=0)
    v1_1 = Arrow([0,0,0],[1,0,0], buff=0)
    v1 = VGroup(v1_0, v1_1)

    v2 = Arrow(E1.c2p(-0.1,-1.5,0),E1.c2p(-3,-1.5,0), buff=0)
    v3 = Arrow(E1.c2p(0.1,-1.5,0),E1.c2p(3,-1.5,0), buff=0)
    v4 = Arrow(E2.c2p(-0.1,-1.5,0),E2.c2p(-3,-1.5,0), buff=0)
    v5 = Arrow(E2.c2p(0.1,-1.5,0),E2.c2p(3,-1.5,0), buff=0)

    n48 = MathTex('G(\\omega t +\\phi) = cos(\\omega t  + \\phi) ').set_color_by_gradient([YELLOW, RED])
    n51 = MathTex('A \\cdot cos(\\omega t  + \\phi) ').set_color_by_gradient([YELLOW, RED])
    n52 = MathTex('g(t)=A \\cdot cos(\\omega \\cdot t  + \\phi) ').set_color_by_gradient([RED, WHITE])

    ####################################################################################################
    #                       PRODUÇÃO CENAS DINÂMICAS
    ####################################################################################################
    #cena 17

    n6.move_to([-1.5,1.5,0])
    G0.move_to([0,0,0]).scale(1.5)
    G1.scale(1.5)
    n9.move_to([1.5,2,0])
    #self.add(G0)
    n7.move_to([0,-3,0])
    #self.add(n7)
    n5.move_to([0,-3,0])
    #self.add(n5)
    n13.move_to(n11)
    #self.add(n13)
    #self.add(n9)
    n42.move_to([2.4,2,0]).scale(1.5)
    #self.add(n42)
    n48.move_to([3,2,0]).scale(1.3)
    #self.add(n48)
    n51.move_to([1.8,2,0]).scale(1.4)
    #self.add(n51)
    n51.move_to([2,2,0]).scale(1.4)
    #self.add(n51)
    n52.move_to([2.8,2,0]).scale(1.5)
    #self.add(n52)

    g1 = VGroup(E1, n10,n11)
    self.play(DrawBorderThenFill(g1), run_time =3)
    self.play(Write(n6), run_time = 3)
    c1_0 = c1.copy().set_color(BLUE)
    self.play(Write(c1_0), run_time = 3)
    self.play(Write(n7), run_time = 3)
    self.play(Transform(n7, n5),Transform(n11, n13),Transform(n6, n9),FadeOut(c1_0),FadeIn(c1), run_time = 2)
    self.wait()
    self.play(Transform(n6, n42), phic1.animate.set_value(1.5), run_time = 2)
    self.wait()
    self.play(Transform(n6, n48), w1.animate.set_value(1.5), run_time = 2)
    self.wait()
    self.play(Transform(n6, n51), Ac1.animate.set_value(2), run_time = 3)
    self.wait()
    self.play(Transform(n6, n52), run_time = 3)
    self.wait(2)
    g2 = VGroup(g1,n6,c1,n7,n11)
    self.play(Unwrite(g2), run_time = 3)
    self.wait()
```




