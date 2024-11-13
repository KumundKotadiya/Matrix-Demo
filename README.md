# Matrix-Demo
demo matrix
import android.graphics.Color
import android.os.Bundle
import android.text.Editable
import android.text.TextWatcher
import android.view.View
import android.widget.Button
import android.widget.EditText
import android.widget.GridLayout
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val inputNumber = findViewById<EditText>(R.id.inputNumber)
        val showMatrixButton = findViewById<Button>(R.id.showMatrixButton)
        val matrixGrid = findViewById<GridLayout>(R.id.matrixGrid)

        showMatrixButton.setOnClickListener {
            val gridSize = inputNumber.text.toString().toIntOrNull() ?: 0
            createMatrix(gridSize, matrixGrid)
        }
    }

    private fun createMatrix(size: Int, grid: GridLayout) {
        grid.removeAllViews()
        grid.columnCount = size
        grid.rowCount = size

        for (i in 0 until size) {
            for (j in 0 until size) {
                val cell = TextView(this).apply {
                    setBackgroundColor(Color.LTGRAY)
                    text = "$i,$j"
                    gravity = android.view.Gravity.CENTER
                    setPadding(10, 10, 10, 10)
                    setOnClickListener {
                        fillRowAndColumn(grid, i, j, size)
                    }
                }
                val params = GridLayout.LayoutParams().apply {
                    rowSpec = GridLayout.spec(i)
                    columnSpec = GridLayout.spec(j)
                    width = 0
                    height = 0
                    setMargins(5, 5, 5, 5)
                    setGravity(android.view.Gravity.FILL)
                }
                grid.addView(cell, params)
            }
        }
    }

    private fun fillRowAndColumn(grid: GridLayout, row: Int, col: Int, size: Int) {
        for (i in 0 until size) {
            val rowView = grid.getChildAt(row * size + i) as TextView
            rowView.setBackgroundColor(Color.YELLOW)
        }
        for (j in 0 until size) {
            val colView = grid.getChildAt(j * size + col) as TextView
            colView.setBackgroundColor(Color.YELLOW)
        }
    }
}
