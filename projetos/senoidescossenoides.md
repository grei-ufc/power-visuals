## Cena 1

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


------------------------------------------------------------------------------------

# Cena 2

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




