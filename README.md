SharpGLES
=========

OpenGL ES 2.0 for .NET Desktop

To use in Windows Forms:

using System;
using System.Windows.Forms;
using SharpGLES;

public partial class GLESForm : Form
{
	private EGLDisplay _display;

	public GLESForm()
	{
		SetStyle(ControlStyles.AllPaintingInWmPaint | ControlStyles.UserPaint, true);
	}

	protected override void OnPaintBackground(PaintEventArgs e)
	{

	}

	protected override void OnPaint(PaintEventArgs e)
	{
		Draw();

		_display.SwapBuffers();

		Invalidate();
	}

	private void Draw()
	{
		GLES20.Viewport(0, 0, Width, Height);

		GLES20.ClearColor(0f, 0f, 0f, 0f);
		GLES20.Clear(GLES20.GL_COLOR_BUFFER_BIT);

		//draw away...
	}

	protected override void OnHandleDestroyed(EventArgs e)
	{
		_display.Dispose();

		base.OnHandleDestroyed(e);
	}

	protected override void OnHandleCreated(EventArgs e)
	{
		base.OnHandleCreated(e);

		_display = new EGLDisplay(Handle);
	}
}